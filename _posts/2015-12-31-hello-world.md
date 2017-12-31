---
layout: post
title: "Hello World!"
date: 2017-12-31 12:00:00 +0100
categories: blog
---

For a while now I have been meaning to start a personal blog. Now, it is finally time to say `Hello World`. 

<!-- more -->

## Introduction and Purpose
For as long as I can remember I've had the desire to express myself and have a creative outlet. I have dabbled in photography, digital art, writing and video. So far nothing really stuck, for one reason or another. I have written fiction stories (or at least attempted to) as well as non-fiction in various forms, such as journaling. Blogging is a logical next step, so here goes. While I am primarily writing for myself, publishing something on the internet challenges me to write differently compared to how I would write in a personal notebook or journal. 

I want this blog to be a place where I can write about ideas and share things that interest me. I also want this website to serve as a place where I can showcase hobby projects that I'm working on; think software projects and photography to name a few. Writing for my eyes only provides a different context and through that, a different purpose. In a personal notebook, I have less incentive to rewrite and edit what I wrote. Through this process, I hope to become a better writer. That being said, I do hope that any projects showcased on this website can be of use to others.

## About this website
This website started out as a bare-bones homepage with hand-crafted HTML that was hosted using GitHub pages. Over the summer I began thinking more seriously about adding a blog to it and adding more pages to it. While looking into content management systems and blogging platforms I came across [Jekyll](https://jekyllrb.com/), an open source static website generator. Jekyll immediately appealed to me because it offers a system that provides everything I need in terms of functionality (so far) while being very flexible, it is light-weight and plain-text based (another plus in my book).


## Jekyll
This website is hosted on GitHub pages. I quite like this as a backend and it makes it easy to have project pages whenever they're needed. It took me a while before I started actually looking into a platform suitable for blogging that could be (easily) coupled with my GitHub page. At first I only needed a basic homepage; meanwhile, I focused on other things such as my first full-time job.

Setting up Jekyll is pretty straightforward, however, there are some dependencies that you need to be aware of. Since I wasn't aware of this at first I got a bit frustrated at some points in the process. In addition, I went through a bit of a learning curve regarding the documentation; most of it seems to be written for people who are already quite well-versed in using Ruby, command-line tools and reading this kind of documentation. For example, I believe that some of the documentation was written with assumptions to the state of the system being worked on, meaning that some necessary dependencies were omitted. The dependencies I ran into on the way were Ruby, RubyGems, nokogiri and Xcode. While OS X ships with Ruby there are a few [reasons](https://robots.thoughtbot.com/psa-do-not-use-system-ruby) why it's advisable not to use the system Ruby. I also made sure RubyGems was up to date. Then, following the [Jekyll quick-start-guide](https://jekyllrb.com/docs/quickstart/) I installed the Jekyll and bundler gems.

```
$ brew install ruby
$ ruby -v
$ gem update --system
$ gem install jekyll
$ gem install bundler
```

I didn't know whether there was an easy way to transform the content I had (handcrafted HTML and CSS) to a Jekyll site. Since I wanted to start with a clean slate and toy around a bit, I decided to clear out the website folder and install Jekyll in it using the standard minima theme.

```
$ rm -rf *
$ jekyll new . 
$ gem install minima
$ jekyll serve --watch
```

At this point, I ran into an issue since nokogiri wasn't installed on my system, so I installed it with the necessary dependencies (see: [nokogiri](http://www.nokogiri.org/tutorials/installing_nokogiri.html#mac_os_x)). Since I updated RubyGems in one of the earlier steps I only needed to update Xcode before installing nokogiri. For good measure, I also installed the [github-pages gem](https://github.com/github/pages-gem) as well.

```
$ gem update --system
$ xcode-select --install
$ gem install nokogiri
```

All in all, this process turned out to be pretty straightforward even though I had to pull information from a number of different sources. Next up I toyed around with themes and layouts, for which [Giraffe Academy's tutorial](https://www.youtube.com/watch?v=T1itpPvFWHI&list=PLLAZ4kZ9dFpOPV5C5Ay0pHaa0RJFhcmcB) proved very helpful. In the end, I decided to stick with the minima theme and to make changes as needed over time. Hence the tagline on my main page.

> This personal website is in permanent beta, it adapts and evolves to reflect my personal growth.