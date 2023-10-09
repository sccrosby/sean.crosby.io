---
title:       "Transitioning to data science"
subtitle:    "My first post, and first steps moving to the data science field from a decade in geoscience"
description: ""
date:        2021-10-11
author:      "Sean C. Crosby"
image:       "me.jpg"
tags:        ["Data Science","Oceanography"]
categories:  []
draft:       true
---

### Re-tooling

This is the beginning of a data odyssey, re-tooling my background in oceanography to the rapidly evolving field of data science. After 10-years in the geosciences I am interested in pursuing something new, faster-paced, and more lucrative. I decided to write this blog, not necessarily expecting anyone to read it, but primarily for my own record keeping as I learn explore a new set of data analysis tools and whatever interesting datasets I can get my hands. I have always enjoyed programming, from my high school education in Visual Studio, to my first foray into java in attempts to test technical analysis trading techniques on stock market data (e.g. MACD, bollinger bands, etc). When I was an undergrad physics major java was still the primarily taught language (alongside C++), but python was beginning to gain ground. As a graduate student, and for the last 10-years I've spent a majority of time with Matlab, the most popular language in geoscience and physical oceanography. Matlab is convenient, but proprietary, and is not the framework of choice in computer- and data- science. Physical oceanography, to its credit, is slowly making the switch to python and I have spent sometime moving small projects to python. Now though is the time to learn modern work-flows (github), big data queries (SQL), and scalable computation (AWS). So here I'll begin.

### Blogging with Github

First I do want to plug Rich Youngkin for putting together this great tutorial on how to use [Hugo](https://gohugo.io/) to create and serve a blog on [Github](https://github.com/). The link is to his blog post is here, https://youngkin.github.io/post/createafreeblogsite/#initialize-the-new-site. And for my own reference I'll add some regularly needed commands to create posts, compile the page, and push to the repo.

- To create a new post, /hugo.exe new post/postXXX.md
- Test site development locally, use *./hugo.exe -D server*
- To compile to public folder use *./hugo.exe -D*
- To push to git use *./deploy.sh*
- For writing markdown, these are useful references: https://www.markdownguide.org/tools/hugo/, https://www.markdownguide.org/extended-syntax/

