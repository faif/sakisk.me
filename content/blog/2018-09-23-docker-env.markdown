---
author: Sakis Kasampalis
date: "2018-09-23T20:00:00Z"
tags:
- docker
- version
- variable
- export
title: Read a version from an external file in a dockerfile
---

I wanted to do a rather simple thing in a dockerfile: read a value from an external file and use it in a `RUN` command.
Doing all this inside the dockerfile was a requirement, so I couldn't pass the version while building the image using `build-args` or a similar solution.

There's nothing hard about achieving this, as long as you keep something in mind: Docker creates intermediate containers
for a lot of things, including `RUN` commands. So that means that everything needs to be done in the same `RUN` pipeline.
The following example shows how we can read a version from an external file and export a variable that we can use (in the
same pipeline).

<script src="https://gist.github.com/faif/98631ee46dc557bdd5ab1dc42abae47f.js"></script>