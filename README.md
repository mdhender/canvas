# CANVAS
The tabula rasa of templates.

Canvas documents how to get a very basic Hugo site up and running on a Mac.
The instructions will work as-is for Linux.
Windows users will need to translate.

# Introduction
Hugo makes creating a new site eally easy, but the site will be useless until you do a bit of work on it.
That's sort of baked into the instructions.
If you run the command with the `--help` flag, Hugo will remind you:

    Michaels-MacBook-Air:mdhender mdhender$ hugo new site --help
    Create a new site in the provided directory.
    The new site will have the correct structure, but no content or theme yet.
    Use `hugo new [contentPath]` to create new content.

This blank slate is helpful if you're experienced and don't want to delete a bit of configuration before building your site, but it can be really rough on beginners just trying to how to get going.

The purpose of this post is to give newbies a leg-up by showing what needs to be done to get to a "working" site.
It's not intended to explain "why" things need to be done (the documentation does a good job of that).

# What you need to know before starting

# Assumptions

## You can run command from the terminal
You will have to use the command line to run Hugo commands.
On the Mac, that means opening Spotlight, typing in "terminal", and double-clicking the `Terminal` application.

Once you've done that, run the following command to confirm that the command line is working:

    Michaels-MacBook-Air:canvas mdhender$ echo hello
    hello

If you don't see the output `hello`, then find someone that can help you access the command line.

## Hugo is installed
Run the command following command to confirm that Hugo is installed:

    Michaels-MacBook-Air:canvas mdhender$ hugo version
    Hugo Static Site Generator v0.55.4/extended darwin/amd64 BuildDate: unknown

If you see something like the following, then Hugo is *not* installed properly.
    -bash: hugo: command not found

## You're comfortable editing text files
You will need to update text files to work with Hugo.
Feel free to use any editor that you're comfortable with (for example, `vi` or `TextEdit`).

# Overview
There's a lot of things.

1. Create the site

# Create the site
When you create a site, the command creates the bare minimum needed to generate a site.
That's a handful of directories and two files.

Run the following command to create our site in a directory named `canvas`:

    Michaels-MacBook-Air:mdhender mdhender$ hugo new site ./canvas
    Congratulations! Your new Hugo site is created in /Users/mdhender/go/src/github.com/mdhender/canvas.

    Just a few more steps and you're ready to go:

    1. Download a theme into the same-named folder.
    Choose a theme from https://themes.gohugo.io/, or
    create your own with the "hugo new theme <THEMENAME>" command.
    2. Perhaps you want to add some content. You can add single files
    with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
    3. Start the built-in live server via "hugo server".

    Visit https://gohugo.io/ for quickstart guide and full documentation.

The first line of the output will contain the path to your site.
Remember it.

## Verify the site was created

Make the `canvas` directory your working directory and confirm that Hugo created the files:

    Michaels-MacBook-Air:mdhender mdhender$ cd canvas
    /Users/mdhender/go/src/github.com/mdhender/canvas
    Michaels-MacBook-Air:canvas mdhender$ ls config.toml archetypes/default.md 
    archetypes/default.md	config.toml

If it did, you're ready to start on the plumbing needed for a basic site.
If it didn't, please go to the Hugo forums to ask for help.

# The plumbing
If you tried generating a site now, you'd get a blank site and warnings like these:

    Michaels-MacBook-Air:canvas mdhender$ hugo server
    Building sites … WARN 2019/04/27 13:45:55 found no layout file for "HTML" for "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
    WARN 2019/04/27 13:45:55 found no layout file for "HTML" for "taxonomyTerm": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
    WARN 2019/04/27 13:45:55 found no layout file for "HTML" for "taxonomyTerm": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.

We're going to create the files that you need for a working site.
These are archetypes, layout files, and content.

# Create an archetypes file
Use your text editor to create the file `archetypes/posts.md` with this content:

    +++
    date = "{{ .Date }}"
    title = "{{ replace .Name "-" " " | title }}"
    type = "post"
    draft = true
    +++

    Lorem ipsum summary.
    <!--more-->
    Lorem ipsum below the fold.

Note the value of the type.
It's singular ("post") while the name of the archetype is plural ("posts").
That'll make sense when we looks at lists of posts.

Also note that I included some sample content in the archetype.
That helps me remember how to split the article for the summary and the content pages.

## section notes
https://gohugo.io/content-management/organization/#index-pages-index-md

# Create a home page
This is content/_index.md

# Create sample content
Create three posts to use for building and testing your site.

Use the `hugo new` command to create the first post:

    Michaels-MacBook-Air:canvas mdhender$ hugo new posts/my-first-post.md
    /Users/mdhender/go/src/github.com/mdhender/canvas/content/posts/my-first-post.md created
    Michaels-MacBook-Air:canvas mdhender$ cat content/posts/my-first-post.md 
    +++
    date = "2019-04-27T13:40:28-06:00"
    title = "My First Post"
    type = "post"
    draft = true
    +++

    Lorem ipsum summary.
    <!--more-->
    Lorem ipsum below the fold.

You can see that Hugo used the archetype file to generate the template.
It added in the date for you and ran a pretty neat conversion on the file name to generate a title.

Create the second post:

    Michaels-MacBook-Air:canvas mdhender$ hugo new posts/my-second-post.md
    /Users/mdhender/go/src/github.com/mdhender/canvas/content/posts/my-second-post.md created
    Michaels-MacBook-Air:canvas mdhender$ cat content/posts/my-second-post.md 
    +++
    date = "2019-04-27T13:40:54-06:00"
    title = "My Second Post"
    type = "post"
    draft = true
    +++

    Lorem ipsum summary.
    <!--more-->
    Lorem ipsum below the fold.

And the third post:

    Michaels-MacBook-Air:canvas mdhender$ hugo new posts/my-third-post.md
    /Users/mdhender/go/src/github.com/mdhender/canvas/content/posts/my-third-post.md created
    Michaels-MacBook-Air:canvas mdhender$ cat content/posts/my-third-post.md 
    +++
    date = "2019-04-27T13:41:09-06:00"
    title = "My Third Post"
    type = "post"
    draft = true
    +++

    Lorem ipsum summary.
    <!--more-->
    Lorem ipsum below the fold.

