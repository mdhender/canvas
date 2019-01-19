---
title: "Basic Single Post Layout"
date: 2019-01-19T16:14:24-07:00
categories: ["posts"]
tags: ["hugo"]
---

The basic post is very similar to the home page we just built.
<!-- more -->

I set the page's title to the post's title.

I removed the `range` loop.
We're only working with a single content file, so it's not needed.

I replaced the `.Summary` with `.Content` to render the entire content file.
I moved it flush with the left margin to make it easier for me to debug the layout from the rendered HTML.
It's not necessary (or even a best practice).

I removed the `nav` and `aside` that linked to other posts.
I want to go over that in a future post.

```
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8" />
	<title>{{ .Title }}</title>
	<link rel="stylesheet" href="/css/canvas.css" type="text/css">
</head>
<body>
    <header>
        <h1><a href="/">Canvas</a></h1>
        <p>the tabula rasa of templates</p>
    </header>
    <nav>
        <ul>
            <li><a href="/">Posts</a></li>
        </ul>
    </nav>

    <main>
        <article>
            <header>
                <h2>{{ .Title }}</h2>
            </header>
{{ .Content }}
        </article>
    </main>

    <footer>
        <ul>
            <li>&copy; 2019 - Michael D Henderson</li>
            <li><a href="https://github.com/mdhender/canvas">Github</a></li>
        </ul>
    </footer>
</body>
</html>
```