---
layout: post
title: "TIL - Implementing a custom serializer for Jackson"
date: 2025-05-28 12:00:00 +0100
categories: blog
tags: [java, spring, json]
---
I am working on a hobby project to play around with my location data as collected through my Garmin watch[^Historical]. For this, I created a Spring (web) project using Java 24, Thymeleaf for templating, Leaflet for data visualisation and JQuery for transforming the data received from Spring. In this process, I ran into some issues with serializing my data and this is how I resolved them.

[^Historical]: I started out using Runkeeper to track my runs, then switched to Strava, until I got my Garmin. So I have some historical data lying around in different formats.

At first, I tried parsing the GPX myself and simply fetched the latitude and longitude from the data. This didn't sit right with me because I didn't feel like creating a whole domain model for stuff that (probably) exists out in the wild. It felt like I would be creating a lot of busywork for myself. So, after looking around on the internet a bit more I found the [jenetics JPX library](https://github.com/jenetics/jpx), which works like a charm[^Runkeeper].

[^Runkeeper]: Runkeeper apparently doesn't create valid GPX files, so I had to parse them using the `lenient` flag.

## The Problem

To get the data from Java objects to a plot in leaflet, I created a REST endpoint and use JQuery to process the data so it can be easily added to Leaflet (I collected bits and pieces I found online, as one does). Here I ran into a bit of trouble because the serialization resulted in an invalid JSON. Now what happened here?

At first, I couldn't wrap my head around what caused the problem and no less how to solve this because JQuery didn't seem to throw any errors. After a bit of debugging I decided to inspect the JSON that my endpoint produced because maybe the issue wasn't with JQuery. So, I figured out that the problem was with serializing the data.

So what does the problem boil down to? A get request in spring returns some data which is serialized using Jackson as a default. This serialization utilizes the `toString()` methods of the objects in question. JPX implements elevation using a custom `Length extends Number` class, which is basically a number with some extra bells and whistles so you can switch between different units (the default is meter). `Length` implements the `toString()` as follows:

```Java
public String toString() {  
    return String.format("%s m", this._value);  
}
```

This results in the following JSON field: `"elevation":2.1 m`. This doesn't work because it's not interpreted as a `String` and can't be interpreted as a number either. And even if it were a `String`, it's not very useful because I want my elevation to be a number (knowing that it represents meters implicitly).

### Intermezzo: GPX Structure

The objects I work with using JPX implement the [GPX format](https://www.topografix.com/gpx.asp). In this format, elevation is part of a Track Point (`WayPoint` in JPX). These are in turn part of Track Segments, which are part of a Track. My current endpoint implementation provides a `List<WayPoint>`.

## Customizing the Serializer

You can customize the serialization process by writing a custom serializer[^Deserialization]. This allows you to define what fields of the object should be serialized and how that should happen. I followed and adapted the example that [springframework guru (aka: JT)](https://springframework.guru/how-to-the-jackson-object-mapper-with-json/) wrote about. This is what my custom serializer looks like:

[^Deserialization]: The same can be done with deserialization.

```Java
public class LengthSerializer extends StdSerializer<Length> {  
  
    public LengthSerializer() {  
        this(null);  
    }  
  
    public LengthSerializer(Class<Length> t) {  
        super(t);  
    }  
  
    @Override
    public void serialize(Length length, JsonGenerator jsonGenerator, SerializerProvider serializerProvider) throws IOException {  
  
        jsonGenerator.writeStartObject();
        jsonGenerator.writeNumberField("elevation", length.doubleValue());
        jsonGenerator.writeEndObject();  
    }  
}
```

In order to use the custom LengthSerializer, you need to register it. Where JT does this as part of his test cases, I prefer doing this registration on its own as follows:

```Java
@Configuration  
class SerializationConfig {  
  
    @Bean  
    public ObjectMapper getObjectMapper() {  

        ObjectMapper objectMapper = new ObjectMapper();  
        SimpleModule simpleModule = new SimpleModule();  

        simpleModule.addSerializer(Length.class, new LengthSerializer());  
        
        objectMapper.registerModule(simpleModule);  
        // Necessary for Optionals
        objectMapper.registerModule(new Jdk8Module());  
        // Necessary for processing dates and times
        objectMapper.registerModule(new JavaTimeModule());  
  
        return objectMapper;  
    }  
}
```

I ran into some errors. Optionals weren't supported out of the box, which is solved by adding the `Jdk8Module` to the `ObjectMapper`. The same goes for working with dates and times, for which I included the `JavaTimeModule`. To be able to use these modules, the following dependencies need to be added to the `pom.xml`:

```xml
<dependency>  
    <groupId>com.fasterxml.jackson.core</groupId>  
    <artifactId>jackson-databind</artifactId>  
    <version>2.18.3</version>  
</dependency>  
  
<dependency>  
    <groupId>com.fasterxml.jackson.datatype</groupId>  
    <artifactId>jackson-datatype-jdk8</artifactId>  
    <version>2.18.3</version>  
</dependency>  
  
<dependency>  
    <groupId>com.fasterxml.jackson.datatype</groupId>  
    <artifactId>jackson-datatype-jsr310</artifactId>  
    <version>2.18.3</version>  
</dependency>
```

This results in the following JSON output for a single `WayPoint` (most fields omitted for clarity).

```json
{
    "elevation":
    {
        "elevation":8.7
    },
    "latitude":52.091126000,
    "longitude":5.110568000
}
```

Because I wrote a custom serializer for the elevation field, I had to provide both a field name and a value, one cannot simply write a number without providing a field name. This results in an undesirable extra level of nesting within the `WayPoint`. The next thing I want to figure out is whether I can create a custom serializer for the `WayPoint`, which only overrides the elevation field.