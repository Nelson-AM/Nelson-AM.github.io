# Hello World!

## Outline
* Introduction
    * Why did I start this blog? Where does this come from?
    * What do I plan to write about? What is the purpose?
* How did I set it up?
    * GitHub pages
    * Jekyll (and getting it to work)

## Intro and Purpose
I've been meaning to start a blog for ages on here and now it is finally time to say `Hello World`.

* This blog serves as a place where I can talk about _things_ that interest me.
    * Projects (code katas, problems / exercises from books)
    * Software projects / programs I make.
    * Cosplay / creative / crafts projects.
    * Thoughts about things.

## Jekyll
This website is hosted through GitHub pages. I quite like this as a backend and it makes it easy to have project pages whenever they're needed. It took me a while before I started actually looking into a platform suitable for blogging that could be (easily) coupled with my GitHub page.

* From hand-made HTML and CSS to Jekyll
* Steps to get Jekyll up and running.
    * Ruby + Gems (why I couldn't use the OSX default Ruby).
    * Installing Jekyll + dependencies.
    * Themes and fine-tuning
    * Sources!

### Setting up Jekyll
Installing Ruby and jekyll (plus dependencies).

```
$ brew install ruby
$ ruby -v
$ gem update --system
$ gem install jekyll
$ gem install bundler
```

Go into directory of github site. I already had a github user page, so I had to clean out the entire directory in order for jekyll to be able to generate a new site.

```
$ rm -rf *

$ jekyll new . 
$ gem install minima

$ jekyll serve --watch
```

There was a problem with nokogiri. I had to install dependencies of nokogiri first (see: http://www.nokogiri.org/tutorials/installing_nokogiri.html#mac_os_x)

```
$ gem update --system
$ xcode-select --install
```

The last commant installs required xcode stuff.

```
$ gem install nokogiri

$ gem install github-pages
```

