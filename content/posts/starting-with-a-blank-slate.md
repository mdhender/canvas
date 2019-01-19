---
title: "Starting with a Blank Slate"
date: 2019-01-17T21:27:13-07:00
categories: ["posts"]
tags: ["hugo"]
---

Canvas is a demonstration of building a site (and a theme) from the ground up.
<!--more-->

Every step of the path is documented as a commit in the [GitHub repo](https://github.com/mdhender/canvas").
I'll try to write a new article explaining the "what" and "why" behind the commit.

If I do a good job, you'll be able to follow the commits and learn the ins-and-outs of Hugo.

## The First Commit

This first commit contains a simple landing page.
The HTML is pretty bloggish with just a hint of formatting.
It uses the CSS from [Normalize.css](https://github.com/necolas/normalize.css) to get a consistent look in browsers.
We'll be adding style later, once we have a theme in place.
The important part (to me) is that it's built up using semantic HTML elements.
It's my belief that makes it easier to build up the site using [Hugo](https://gohugo.io).

## The Footer

The footer of the article is links for navigating between articles.

The only complicated bit is the categories and tags.
I think of category as topic (or "filed under") and tags as keywords for searching.
That will come up when we start
