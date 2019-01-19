---
draft: true
title: "Creating a Post Archetype"
date: 2019-01-19T09:23:18-07:00
categories: ["posts"]
tags: []
---

My goal this morning is to create an archetype file for posts.
I want to be able to do something like:

```
$ hugo new posts/creating-a-post-archetype.md
```

From the previous post, we know that Hugo will look for `archetypes/posts.md`.

It feels weird to me to use `posts` to create a single `post`.
If I wanted, I could do:

```
$ hugo new --kind=post posts/creating-a-post-archetype.md
```

That would tell Hugo to look for `archetypes/post.md`.

The tradeoff is the clunkier command line.
It would be great if Hugo translated the plural to the single here (it actually does in other places).
It doesn't, so I'll work with the shorter command line.

## Creating the archetype file

My posts archetype is updates the default archetype template by adding categories and tags:

```
$ cat archetypes/posts.md
---
draft: true
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
categories: ["posts"]
tags: []
---
```

I also moved `draft` up to the top.
That will help remind me to delete the flag when I'm ready to publish.

I added `categories` and `tags` with a default value.
That will help keep me organized as my content builds up.

## Themes

You may have noticed that I'm creating my files in the site's root directory instead of in a theme directory.
You may have even wondered, "Why?"

* It's easier at first to work from the root.
* Hugo always looks for files in the root before the theme so I always know where to look.
* I don't have to navigate between as many directories to update files.
* I don't have the extra step of running `hugo new theme`.
* And it's really easy to create a theme by moving files from the root.

### Postscript: Cleaning up

I edited the first two posts and linked this one in.
I really need to automate that!