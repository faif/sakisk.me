+++
title = 'Posting to LinkedIn and Bluesky programmatically'
date = 2025-01-10T11:16:22+01:00
draft = false
tags = [ "LinkedIn", "Bluesky", "social media", "API", "python", "program" ]
+++

![Bluesky](/assets/bluesky.jpeg)

## Background

Whenever I have something to share with the world (mainly technical content), I post it on social media so that other
people can also check it out. I usually post about articles and books that I've read, new blogposts that I've
written, and discounts on my book. The two social media platforms I was using until now were LinkedIn and X (former
Twitter). But it's time to replace X with something else, for administrative purposes...

## The problem

When X was still named Twitter, it offered a public API. That made it possible to create a new post on LinkedIn and
configure LinkedIn to also post the same content to Twitter. Posting to only one social media platform and reposting
to others is very convenient. Sadly, this is not possible anymore for X, because X does no longer offer a public API.
That annoys me, thus I've decided to replace X with Bluesky, and write a program that supports posting to both
platforms using their APIs. An extra benefit of switching to Bluesky is that it doesn't have ads (so far); I'm not a
big fan of ads.

## LinkedSky

I wrote a free software terminal-based Python program that allows me to post both to LinkedIn and Bluesky, without
needing to use a Web Browser and interact with their Web <abbr title="User Interface">UI</abbr>. Source code and
documentation are available on GitHub: [LinkedSky repo](https://github.com/faif/linkedsky).
