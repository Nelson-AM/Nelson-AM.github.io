---
layout: post
title: "Regex in Java: Matching Line Breaks With a Dot"
date: 2020-05-07 12:00:00
categories: blog
tags: java regex
---

Last week I set out to write some unit-tests for a Java application. Because the assertions target variable fields in a JSON string, I decided to use regular expressions (regex) to match these fields. In doing this, I learned a few interesting things, which weren't immediately obvious to me, about how regex are implemented in Java.

<!-- more -->

Based on my experience with regex in Python, I started with the following code snippet. In this example, I want to assert whether the `key: value` pair is present anywhere in the `exampleJsonString` (which contains line breaks).

```java
// Assign exampleJsonString and exampleRegex for clarity
String exampleJsonString = "{\n key : value, \n(...)\n}";
String exampleRegex = ".*key : value.*";
assertTrue(exampleJsonString.matches(exampleRegex));
```

This did not work because in Java's implementation of regex the dot-wildcard `.` does not include line terminators. This behaviour wasn't immediately obvious to me and it took a while to figure out that this is implemented in some flavours of regex. To cite the [Java 14 docs on regex](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/regex/package-summary.html):

> Predefined character classes
>
> .   Any character (may or may not match line terminators)

With line-terminators being defined as:

> A line terminator is a one- or two-character sequence that marks the end of a line of the input character sequence. The following are recognized as line terminators:
>
> * A newline (line feed) character ('\n'),
> * A carriage-return character followed immediately by a newline character ("\r\n"),
> * A standalone carriage-return character ('\r'),
> * A next-line character ('\u0085'),
> * A line-separator character ('\u2028'), or
> * A paragraph-separator character ('\u2029').

There are two ways to get around this limitation. The first way I found uses `Pattern.compile()` to compile the regex into an instance of the `Pattern` class. This allows you to pass the `Pattern.DOTALL` flag, which makes the `.` match any character including line breaks, as follows:

```java
String exampleJsonString = "{\n key : value, \n(...)\n}";
Pattern exampleRegex = Pattern.compile(".*key : value.*", Pattern.DOTALL)
assertTrue(exampleRegex.matcher(testJson).find());
```

Alternatively, the `Pattern.DOTALL` mode can be enabled via the embedded flag expression `(?s)`. According to the docs '\[t\]he `s` is a mnemonic for "single-line" mode, which is what this is called in Perl'. This results in:

```java
String exampleJsonString = "{\n key : value, \n(...)\n}";
String exampleRegex = "(?s).*key : value.*";
assertTrue(exampleJsonString.matches(exampleRegex));
```

While both solutions exhibit the same functional behaviour, each has its benefits. The first solution performs better; executing the assertion 1 million times in a test method takes 251 ms for the first against 509 ms for the second. The second solution is closer to what I started with and feels more straightforward to me. Embedded flags can be used on specific parts of the regex, such as within a capture group at the expense of making the regex potentially harder to read; this holds for both compiled and uncompiled regex.

## The Double-Escape

I'll end with a short note on string compilation. Java compiles strings, which mean that escaping characters in regex requires some close attention. Say, I want to match a digit using `\d`, escaping it with a single `\` means the Java compiler interprets it as an escape character (depending on language level this can even be considered illegal) instead of interpreting it as part of a regex. So instead, to construct a **regex** to match a digit `String regex = "\d";`, we need to construct the literal `\` preceding a `d`, as such: `String regex = "\\d";`. While this is a rather simple example, you can end up with quite a few backslashes and a complaining IDE.
