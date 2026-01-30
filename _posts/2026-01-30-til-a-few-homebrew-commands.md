---
layout: post
title: "TIL: A Few Homebrew Commands"
date: 2026-01-30 10:00:00 +0100
categories: blog
tags: [macos, homebrew]
---

I've been running into issues when upgrading [Docker](https://www.docker.com/) on my work machine, so I want to prevent Docker from upgrading until I ~~have~~ make time to figure out the issues (or hope that they resolve themselves).

<!-- more -->

Aside from ignoring the notifications in my company's self-service portal, some components have been installed by [homebrew](https://brew.sh/).

- `brew pin <formula>` pins the formula so `brew upgrade` ignores it.
- `brew list --pinned` for if at some point, I want to know which formulas I have pinned.

Credit where credit's due: [stackoverflow](https://stackoverflow.com/questions/10093918/how-to-tell-brew-to-skip-one-formula-when-doing-brew-upgrade).
