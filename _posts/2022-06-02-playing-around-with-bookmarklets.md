---
layout: post
title: "Playing Around With Bookmarklets"
date: 2022-06-02 12:00:00
categories: blog
tags: bookmarks web javascript
---

Years ago, I discovered a bookmarklet that allowed you to fill in a Jira ticket ID, and it would redirect you to that ticket in a separate tab. This was back at a previous job where Jira was used. In the meantime, I have worked at a few places where other tools were used. Now I'm back at a job where Jira is used so I dug it back up. I also started playing around with bookmarklets to make life easier in other ways.

<!-- more -->

## The Jira bookmarklet

The Jira bookmarklet I found is courtesy of Matita. In their [blog post](https://matita.github.io/2015/10/23/go-to-jira-bookmarklet/), Matita explains their reasons for liking and using bookmarklets. What resonates most with me is the autonomy that comes with bookmarklets. If you want to skip directly to the code, it's on [Github](https://github.com/matita/gotojira-bookmarklet).

## Quick Confluence search

I like Confluence as a wiki, but their search functionality isn't the best. I'm not talking about the quality and ordering of search results but the fact that the default behaviour is for search to run in a sidebar. This makes it feel unwieldy if you want to interact with multiple pages or need to go back and forth between results. How to make this easier to use?

Confluence has an advanced search that runs as a separate web page, meaning it has a URL I can use. With this, I only need this bookmarklet to do three things: (1) display a pop-up with a prompt, (2) build the URL by combining a base URL with the search text and (3) navigate to the page, which turns into this little bit of code.

```javascript
javascript: (
function(){
    var search_text;
    var base_url = 'https://confluence.<yourcompany>.com/dosearchsite.action?cql=siteSearch%20~%20%22';
    var params = '%22&includeArchivedSpaces=false';
    if (!search_text) search_text = prompt('Write your Confluence search query');

if (search_text) {
var url = base_url + search_text + params;
window.open(url)
}
})();
```

To use this bookmarklet, you only need to change the base URL. Then create a new bookmark and paste this code into the URL field.

---

2024-01-31: Fixed a bug in the Confluence bookmarklet.
