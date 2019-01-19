---
title: "Basic Home Page"
date: 2019-01-19T13:58:46-07:00
categories: ["posts"]
tags: ["hugo"]
---

I want my home page to show a list of my posts with the newest posts listed first.
<!--more-->

The layout for this uses sections to wrap the summary:

```
<section>
    <header>
        <h2>Post Title</h2>
    </header>
    <p>Post Summary</p>
    <nav>
        <ul>
            <li><a href="Post Link">Read More &raquo;</a></li>
        </ul>
    </nav>
</section>
```

For each summary, we need to

1. Replace "Post Title" with the real title.
1. Replace "Post Summary" with a summary of the post.
1. Replace "Post Link" with a link to the full post.

Fortunately for us, Hugo has variables for each of these.

```
<section>
    <header>
        <h2>{{ .Title }}</h2>
    </header>
    {{ .Summary }}
    <nav>
        <ul>
            <li><a href="{{ .Permalink | relURL }}">Read More &raquo;</a></li>
        </ul>
    </nav>
</section>
```

The `relURL` is a template function that fixes up a URL.
You can look in the Hugo [documentation](https://gohugo.io/documentation/) for more information.

To get a list of posts, we have to use the "range" method.
That method runs a query against a set of data and calls our template code once for each bit of data.

I'm going to jump ahead and just say that the template variable `.Pages` contains all of the content for the site.

```
{{ range where .Pages.ByPublishDate.Reverse "Section" "posts" }}
<section>
    <header>
        <h2>{{ .Title }}</h2>
    </header>
    {{ .Summary }}
    <nav>
        <ul>
            <li><a href="{{ .Permalink | relURL }}">Read More &raquo;</a></li>
        </ul>
    </nav>
</section>
{{ end }}
```

As I mentioned, `.Pages` is the set of all the content in the site.
Adding `.ByPublishDate.Reverse` to it sorts that set by the post's publish date.

The value `"Section"` tells the range method to only grab a single kind of content.
In this case, that's all posts.

Let's update our `layouts/index.html` to have our main and sidebar to look like:

```
<main>
    {{ range where .Pages.ByPublishDate.Reverse "Section" "posts" }}
        <section>
            <header>
                <h2>{{ .Title }}</h2>
            </header>
            {{ .Summary }}
            <nav>
                <ul>
                    <li><a href="{{ .Permalink | relURL }}">Read More &raquo;</a></li>
                </ul>
            </nav>
        </section>
    {{ end }}
</main>

<aside>
    <section>
        <h4>Recent Posts</h4>
        <nav>
            <ul>
            {{ range where .Pages.ByPublishDate.Reverse "Section" "posts" }}
                <li><a href="{{ .Permalink | relURL }}">{{ .Title }}</a></li>
            {{ end }}
            </ul>
        </nav>
    </section>
</aside>
```

When we use `hugo server --buildDrafts` (remember, we need the drafts flag since the posts have `draft: true` in them),
our home page will have a list of the posts.

It's not perfect - the "Read More" links are broken and the summary includes block quotes.
That's work for some future posts.

### Postscript: Template Engine

Hugo uses the [Go template engine](https://golang.org/pkg/html/template/) with some customizations to make it easier to use.
