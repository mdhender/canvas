---
draft: true
title: "Hello Template"
date: 2019-01-19T12:24:22-07:00
categories: ["posts"]
tags: []
---

Today I'm going to build a simple home page template for my site.

The home page is the big, splashy "you're here!" page.
It's the first page that visitors see, so it usually has a different layout than any other page on your site.
I use it to show summaries of recent posts, information on the site, and links to other content.

The template for the home page is stored in `layouts/index.html`.
Other than the name, there's nothing special about the template.
It has the same access to site variables and content as any other page.

## Home Page Layout

The page is going to show a banner, a navigation bar, a list of recent posts, and a copyright footer:

```
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8" />
	<title>Canvas</title>
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
        <section>
            <header>
                <h2>Post One Title</h2>
            </header>
            <p>Post Summary</p>
            <nav>
                <ul>
                    <li><a href="/">Read More &raquo;</a></li>
                </ul>
            </nav>
        </section>

        <section>
            <header>
                <h2>Post Two Title</h2>
            </header>
            <p>Post Summary</p>
            <nav>
                <ul>
                    <li><a href="/">Read More &raquo;</a></li>
                </ul>
            </nav>
        </section>
    </main>

    <aside>
        <section>
            <h4>Recent Posts</h4>
            <nav>
                <ul>
                    <li><a href="/creating-a-post-archetype.html">Creating a Post Archetype</a></li>
                    <li><a href="/first-look-at-archetypes.html">A First Look at Archetypes</a></li>
                    <li><a href="/newsite.html">Initializing the site with Hugo</a></li>
                    <li><a href="/">Home</a></li>
                </ul>
            </nav>
        </section>
    </aside>
      
    <footer>
        <ul>
            <li>&copy; 2019 - Michael D Henderson</li>
            <li><a href="https://github.com/mdhender/canvas">Github</a></li>
        </ul>
    </footer>
</body>
</html>
```

Note that the articles are just placeholders.
Since there's no template logic in the layout, Hugo copies it as is.

### Postscript: Credits

This layout is inspired by [Bruce Lawson](http://html5doctor.com/designing-a-blog-with-html5/) and [Robert Siemer](https://stackoverflow.com/questions/4781077/html5-best-practices-section-header-aside-article-elements).

### Postscript: Bad Title

I apologize for the title.
I was thinking "Hello World" for templates.

### Postscript: Cleaning Up

The landing page is created as `index.html`.
That conflicts with my original `static/index.html`, so I renamed it to `static/blank-slate.html` and updated links in the other static HTML files.

