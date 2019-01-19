---
title: "First Look at Archetypes"
date: 2019-01-18T15:47:35-07:00
categories: ["posts"]
tags: ["hugo"]
---

This post is about archetype files.
Probably too much information, but it all starts with the archetype.
<!--more-->

## What's an Archetype file?

Archetypes live in the `archetypes/` directory in the root of your site.
Hugo automatically creates a file there, `default.md`.

  $ ls -l archetypes/
  total 8
  drwxr-xr-x   3 mdhender  staff  102 Jan 18 20:17 .
  drwxr-xr-x  10 mdhender  staff  340 Jan 18 20:29 ..
  -rw-r--r--   1 mdhender  staff   84 Jan 18 20:17 default.md

That file contains just enough information to get by:

  $ cat archetypes/default.md 
  ---
  title: "{{ replace .Name "-" " " | title }}"
  date: {{ .Date }}
  draft: true
  ---

As you build up your site, you'll create other archetype files to match your workflow.

## What's it used for?

Hugo use an archetype file as a template when you use the `hugo new` command to create content.
That's right - Hugo actually uses the path you give it to render the archetype file into the content file you asked for.

## How does Hugo determine which archetype to use?

The rule of thumb is that the first part of the path is used as the archetype.
If Hugo can't find a matching file, it looks for a default file.

For example, with the command `hugo new posts/first-look-at-archetypes.md`, Hugo uses `posts` as the archetype and `.md` as the extension.
It would first look for `posts.md` and then for `default.md`.

The exact rules are as follows.

1. Use a file name based on the kind of archetype and the extension given.
For example, `hugo new posts/my-first-post.md` would look for a file named `posts.md`.
1. Look in the site's `archetypes/` directory.
If the file is found, use it and stop looking.
1. Look in the theme's `archetypes/` directory.
If the file is found, use it and stop looking.
1. Change the file name we're looking for.
Instead of the archetype, use a file name based of `default` and the extension given.
For example, `hugo new posts/my-first-post.md` would look for a file named `default.md`.
1. Look in the site's `archetypes/` directory.
If the file is found, use it and stop looking.
1. Look in the theme's `archetypes/` directory.
If the file is found, use it and stop looking.
1. Otherwise, use the internal archetype template.
It should be familiar by now - it's the one used to create the `archetypes/default.md` when you created the site.

There's some additional logic that wraps up the site's language code.
We'll get to that in a later post when we talk about mult-lingual sites.

If these rules fail to use the archetype template that you want, use the `--kind` flag to override Hugo's logic.

Hugo uses archetype files when you create new content.

## Generating Content

The command `hugo new` uses the archetype file to create new content.
I used it to generate the file for this post:

  $ hugo new posts/first-look-at-archetypes.md
  /Users/mdhender/Sites/canvas/content/posts/first-look-at-archetypes.md created

The filename, `posts/first-look-at-archtypes.md`, tells Hugo to create a file named `first-look-at-archetypes.md` in the `contents/posts/` folder.

  $ ls -l content/posts
  total 8
  -rw-r--r--  1 mdhender  staff   87 Jan 18 15:47 first-look-at-archetypes.md

Hugo requires that all content be saved under `content/`, so I don't need to add that on the command line.
(The extension `.md` is for my benefit - it means that I'll be writing Markdown.)

Note that Hugo is kind enough to create the directory if it doesn't already exist.

### Content Bug

Currently there's a bug in Hugo.
If you specify an archetype kind that matches a directory in your site's root, Hugo will create the content there.
It's annoying, so avoid archetypes names of

1. archetypes
1. content
1. data
1. layouts
1. public
1. static
1. themes

## Sensible Defaults

I like to say that Hugo was written by lazy coders.
I don't mean that they took shortcuts.
What I mean is that the developers wrote Hugo to save time.
The result is that when Hugo creates the file, it doesn't create a blank file.
It files out the file with some intial values to save you the trouble of typing them yourself.

  ---
  title: "First Look at Archetypes"
  date: 2019-01-18T15:47:35-07:00
  draft: true
  ---

Hugo converted the file name to a title, adds a date, and sets a flag so that the post won't be published before you're ready.

### Title

I think that it's nice that Hugo converts "first-look-at-archetypes.md" to "First Look at Archetypes."
It saves me a little typing on each post (and removes one excuse for not posting).

Hugo turns a file name into a title by removing the extension, changing hyphens to spaces, and running the result through a routine that converts words to "title case."

What's really impressive is that this works for many languages, not just English.

I don't like starting the file names with "a-" (it's personal), but I want that in the title, so I'm going to update the title:

  ---
  title: "A First Look at Archetypes"
  date: 2019-01-18T15:47:35-07:00
  draft: true
  ---

### Date

Hugo uses the clock from your computer to set the date.
That means that you automatically get the right time zone.
This date is used as a default value for a few other dates when Hugo generates your site.
We'll go into detail on that in a future post.

### Draft

Draft is a flag that tells Hugo if the post is ready to be published.

When the flag is set to true, Hugo won't render the post unless you pass the `--buildDraft` flag on the command line when you're building your site.

Some people don't like having this flag set to true.
Others like the protection it provides.
Whether it's friend or foe is up to you.
Either way, Hugo provides an easy way for you to decide.
That's through the "magic" of archetype files.

### Postscript: Cleaning up

I edited the first two posts and linked this one in.
I really need to automate that!

### Postscript: Some Git Notes
I just realized that there is some value in committing the public/ folder.
It makes it easier for you to see what the site looks like after each step.
So I've removed `public/` from my `.gitignore` file.

