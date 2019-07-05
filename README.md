# CANVAS
The tabula rasa of templates.

Canvas documents how to get a very basic Hugo site up and running on a Mac.
The instructions will work nearly as-is for Linux.
Windows users will need to translate.

# Introduction
Hugo makes creating a new site really easy, but the site will be useless until you do a bit of work on it.
That's sort of baked into the instructions.
If you run the command with the `--help` flag, Hugo will remind you:

    $ hugo new site --help
    Create a new site in the provided directory.
    The new site will have the correct structure, but no content or theme yet.
    Use `hugo new [contentPath]` to create new content.

This blank slate is helpful if you're experienced and don't want to delete a bit of configuration before building your site, but it can be really rough on beginners just trying to how to get going.

The purpose of this post is to give newbies a leg-up by showing what needs to be done to get to a "working" site.
It's not intended to explain "why" things need to be done (the documentation does a good job of that).

# Assumptions

## You can run commands from the terminal
You will have to use the command line to run Hugo commands.

## MacOS
On the Mac, that means opening Spotlight, typing in "terminal", and double-clicking the `Terminal` application.

Once you've done that, run the following command to confirm that the command line is working:

    $ echo hello
    hello

If you don't see the output `hello`, then find someone that can help you access the command line.

## Windows
On Windows, click the Start button and type "Powershell" (without the quotes), and then click the Powershell tile. (Full instructions are available [here](https://docs.microsoft.com/en-us/powershell/scripting/getting-started/starting-windows-powershell?view=powershell-6).)

    C:\Users\mdhender> echo hello
    hello

Once you've done that, run the following command to confirm that the command line is working:

If you don't see the output `hello`, then find someone that can help you access the command line.

## Hugo is installed
Run the command following command to confirm that Hugo is installed:

    $ hugo version
    Hugo Static Site Generator v0.55.4/extended darwin/amd64 BuildDate: unknown

If you see something like the following, then Hugo is *not* installed properly.
    -bash: hugo: command not found

## You're comfortable editing text files
You will need to update text files to work with Hugo.
Feel free to use any editor that you're comfortable with (for example, `vi` or `TextEdit`).

# Overview
We're going to create a simple site for bloggers.
1. The home page will show recent posts.
2. We'll have two sections, one for posts and one for articles.
3. There's no difference between posts and articles; I'm doing this just to show how sections work.

# Create the site
When you create a site, the command creates the bare minimum needed to generate a site.
That's a handful of directories and two files.

Run the following command to create our site in a directory named `canvas`:

    $ hugo new site ./canvas
    Congratulations! Your new Hugo site is created in /home/mdhender/go/src/github.com/mdhender/canvas.

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

    $ cd canvas
    /home/mdhender/go/src/github.com/mdhender/canvas
    $ ls config.toml archetypes/default.md
    archetypes/default.md	config.toml

If it did, you're ready to start on the plumbing needed for a basic site.
If it didn't, please go to the Hugo forums to ask for help.

# The plumbing
If you tried generating a site now, you'd get a blank site and warnings like these:

    $ hugo server
    Building sites … WARN 2019/04/27 13:45:55 found no layout file for "HTML" for "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
    WARN 2019/04/27 13:45:55 found no layout file for "HTML" for "taxonomyTerm": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
    WARN 2019/04/27 13:45:55 found no layout file for "HTML" for "taxonomyTerm": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.

We're going to create the files that you need for a working site.
These are archetypes, layout files, and content.

# Update the site's configuration file
The `config.toml` is located in your site's top directory.
By default, it looks something like this:

    baseURL = "http://example.org/"
    languageCode = "en-us"
    title = "My New Hugo Site"

Change that file to reflect the particulars of your site.
In my case, that's:

    baseURL = "https://canvas.mdhender.dev/"
    languageCode = "en-us"
    title = "A Blank Site"
    disableKinds = ["taxonomy", "taxonomyTerm"]

(Note that I slipped in the option to disable taxonomy.
This walkthrough doesn't provide templates for taxonomies, so Hugo generates a warning.
Disabling it seems like a reasonable approach.)

# Create a style sheet for the site
Create a style sheet:

    $ cat static/css/canvas.css
    html {
        background-color: #fefefe
    }

    body {
        color: #454545;
        font-size: 18px;
        margin: 2em auto;
        max-width: 800px;
        padding: 1em;
        line-height: 1.6;
    }

    h1, h2, h3 {
        line-height:1.2
    }

    a {
        color: #07a
    }

    a:visited {
        color: #941352
    }

I know, it's terrible.
That's because it's only here to show how to add style sheets to the site.

# Create archetype files
Archetype files are used when you generate content.

We're going to create two archetype files, one for posts and another for articles.
We're only doing this to show how to use sections.

Use your text editor to create the file `archetypes/posts.md` with this content:

    +++
    date = "{{ .Date }}"
    title = "{{ replace .Name "-" " " | title }}"
    type = "post"
    draft = true
    +++

    Lorem ipsum summary of the post.
    <!--more-->
    Lorem ipsum rest of the post.

Note the value of the type.
It's singular ("post") while the name of the archetype is plural ("posts").
That'll make sense when we looks at lists of posts.

Also note that I included some sample content in the archetype.
That helps me remember how to split the article for the summary and the content pages.

Now do the same to create the file `archetypes/articles.md`:

    +++
    date = "{{ .Date }}"
    title = "{{ replace .Name "-" " " | title }}"
    type = "article"
    draft = true
    +++

    Lorem ipsum summary of the article.
    <!--more-->
    Lorem ipsum rest of the article.

# Create sample content
Use the `hugo new` command to create three posts and three articles to use for building and testing your site.

    $ hugo new posts/my-first-post.md
    /home/mdhender/go/src/github.com/mdhender/canvas/content/posts/my-first-post.md created

    $ hugo new articles/my-first-article.md
    /home/mdhender/go/src/github.com/mdhender/canvas/content/articles/my-first-article.md created

    $ hugo new posts/my-second-post.md
    /home/mdhender/go/src/github.com/mdhender/canvas/content/posts/my-second-post.md created

    $ hugo new articles/my-second-article.md
    /home/mdhender/go/src/github.com/mdhender/canvas/content/articles/my-second-article.md created

    $ hugo new posts/my-third-post.md
    /home/mdhender/go/src/github.com/mdhender/canvas/content/posts/my-third-post.md created

    $ hugo new articles/my-third-article.md
    /home/mdhender/go/src/github.com/mdhender/canvas/content/articles/my-third-article.md created

Let's confirm that the correct archetypes were used.
When we view the files, the type should match the path to the file (e.g., posts should have a type of "post").

    $ cat content/posts/my-first-post.md
    +++
    date = "2019-04-27T15:07:22-06:00"
    title = "My First Post"
    type = "post"
    draft = true
    +++

    Lorem ipsum summary of the post.
    <!--more-->
    Lorem ipsum rest of the post.

    $ cat content/articles/my-first-article.md
    +++
    date = "2019-04-27T15:07:32-06:00"
    title = "My First Article"
    type = "article"
    draft = true
    +++

    Lorem ipsum summary of the article.
    <!--more-->
    Lorem ipsum rest of the article.

You can see that Hugo used the archetype file to generate the template.
If you don't, then there's a problem with how you created the archetype files.
Look for mispellings (the name must match the path in `content`).
If you're stumped, try asking for help in the Hugo forums.

Note that Hugo added in the date for you and ran a pretty neat conversion on the file name to generate a title.

# Create a home page
The home page (or landing page or root page) is created from the file `content/_index.md`.

Use the `hugo new` command to create it:

    $ hugo new _index.md
    /home/mdhender/go/src/github.com/mdhender/canvas/content/_index.md created

The file is not very useful as is:

    $ cat content/_index.md
    ---
    title: ""
    date: 2019-04-27T15:29:04-06:00
    draft: true
    ---

Edit the file.
Go ahead and update the title, remove the `draft` flag, and add some content to it:

    ---
    title: "Home Sweet Home"
    date: 2019-04-27T15:29:04-06:00
    ---

    I like home pages.

# Create templates
Templates are used to render content.
We have

Note that I'm going to create two partials, head and foot, to hold some common HTML.

Use your editor to create the following files.
## layouts/index.html
    {{ partial "head.html" . }}

    <main>
    <section>
        <!-- this section is populated from content/_index.md -->
        <header>
        <h1>{{.Title}}</h1>
        </header>

        <article>
        {{.Content}}
        </article>

        <footer>
        <!-- Note that .Pages is the same as .Site.RegularPages on the homepage template. -->
        {{ range first 10 .Pages }}
            {{ .Render "summary"}}
        {{ end }}
        </footer>
    </section>

    <section>
        <!-- this section is populated by pulling posts from the site -->
        {{ range first 1 (where .Pages.ByPublishDate.Reverse "Section" "posts") }}
            <article>
                <header>
                <h2>{{ .Title }}</h2>
                <p><time datetime="{{.Date}}">{{ .Date.Format "Mon, Jan 2, 2006" }}</time></p>
                </header>
                {{ .Summary }}
                <nav>
                <ul>
                    <li><a href="{{ .RelPermalink }}">Read More &raquo;</a></li>
                </ul>
                </nav>
            </article>
        {{ end }}
        <footer>
        <a href="{{ "posts/" | absURL }}">All posts...</a>
        </footer>
    </section>

    <section>
        <!-- this section is populated by pulling articles from the site -->
        {{ range first 1 (where .Pages.ByPublishDate.Reverse "Section" "articles") }}
            <article>
                <header>
                <h2>{{ .Title }}</h2>
                <p><time datetime="{{.Date}}">{{ .Date.Format "Mon, Jan 2, 2006" }}</time></p>
                </header>
                {{ .Summary }}
                <nav>
                <ul>
                    <li><a href="{{ .RelPermalink }}">Read More &raquo;</a></li>
                </ul>
                </nav>
            </article>
        {{ end }}
        <footer>
        <a href="{{ "articles/" | absURL }}">All articles...</a>
        </footer>
    </section>
    </main>

    {{ partial "foot.html" .}}
## layouts/article/single.html
    {{ partial "head.html" . }}

    <main>
    <section>
        <header>
        <h1>{{.Title}}</h1>
        </header>

        <article>
        {{.Content}}
        </article>

        <footer>
                <ul>
                    {{ with .PrevInSection }}<li><a href="{{ .Permalink }}">&laquo; {{ .Title }}</a></li>{{ end }}
                    {{ with .NextInSection }}<li><a href="{{ .Permalink }}">{{ .Title }} &raquo;</a></li>{{ end }}
                </ul>
        </footer>
    </section>
    <aside>
        <ul>
        <li><a href="{{ .Site.BaseURL }}">Home</a></li>
        <li><a href="{{ "posts/" | absURL }}">Posts</a></li>
        <li><a href="{{ .Section | absURL }}">Articles</a></li>
        </ul>
    </aside>
    </main>

    {{ partial "foot.html" .}}
## layouts/articles/list.html
    {{ partial "head.html" . }}

    <main>
    <section>
        <header>
        <h1>All Articles</h1>
        </header>

        <article>
        <ul>
            {{ range where .Pages.ByPublishDate.Reverse "Section" "articles" }}
            <li><a href="{{ .RelPermalink }}">{{ .Title }} - <time datetime="{{.Date}}">{{ .Date.Format "2006/01/02 15:04:05" }}</time></a></li>
            {{ end }}
        </ul>
        </article>
    </section>

    <aside>
        <ul>
        <li><a href="{{ .Site.BaseURL }}">Home</a></li>
        <li><a href="{{ "posts/" | absURL }}">Posts</a></li>
        <li><a href="{{ "articles/" | absURL }}">Articles</a></li>
        </ul>
    </aside>
    </main>

    {{ partial "foot.html" .}}
## layouts/partials/foot.html
    <footer>
        <ul>
            <li><a href="https://github.com/mdhender/canvas">Github</a></li>
        </ul>
    </footer>
    </body>
    </html>
## layouts/partials/head.html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <title>Canvas</title>
      <link rel="stylesheet" href="/css/canvas.css" type="text/css">
    </head>
    <body>
## layouts/post/single.html
    {{ partial "head.html" . }}

    <main>
    <section>
        <header>
        <h1>{{.Title}}</h1>
        </header>

        <article>
        {{.Content}}
        </article>

        <footer>
                <ul>
                    {{ with .PrevInSection }}<li><a href="{{ .Permalink }}">&laquo; {{ .Title }}</a></li>{{ end }}
                    {{ with .NextInSection }}<li><a href="{{ .Permalink }}">{{ .Title }} &raquo;</a></li>{{ end }}
                </ul>
        </footer>
    </section>
    <aside>
        <ul>
        <li><a href="{{ .Site.BaseURL }}">Home</a></li>
        <li><a href="{{ .Section | absURL }}">Posts</a></li>
        <li><a href="{{ "articles/" | absURL }}">Articles</a></li>
        </ul>
    </aside>
    </main>

    {{ partial "foot.html" .}}
## layouts/posts/list.html
    {{ partial "head.html" . }}

    <main>
    <section>
        <header>
        <h1>All Posts</h1>
        </header>

        <article>
        <ul>
            {{ range where .Pages.ByPublishDate.Reverse "Section" "posts" }}
            <li><a href="{{ .RelPermalink }}">{{ .Title }} - <time datetime="{{.Date}}">{{ .Date.Format "2006/01/02 15:04:05" }}</time></a></li>
            {{ end }}
        </ul>
        </article>
    </section>

    <aside>
        <ul>
        <li><a href="{{ .Site.BaseURL }}">Home</a></li>
        <li><a href="{{ "posts/" | absURL }}">Posts</a></li>
        <li><a href="{{ "articles/" | absURL }}">Articles</a></li>
        </ul>
    </aside>
    </main>

    {{ partial "foot.html" .}}

# View your site locally
Now's a good time to mention that all of the content we created
had the `draft` flag set to true.
That means that Hugo will not show it unless you add the `--buildDrafts` flag
to the command line!

Let's do that now:
    $ hugo server --buildDrafts

                    | EN
    +------------------+----+
    Pages            | 12
    Paginator pages  |  0
    Non-page files   |  0
    Static files     |  1
    Processed images |  0
    Aliases          |  0
    Sitemaps         |  1
    Cleaned          |  0

    Total in 7 ms
    Watching for changes in /home/mdhender/go/src/github.com/mdhender/canvas/{content,layouts,static}
    Watching for config changes in /home/mdhender/go/src/github.com/mdhender/canvas/config.toml
    Environment: "development"
    Serving pages from memory
    Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
    Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
    Press Ctrl+C to stop

We used `server`, so Hugo is running a web server on your computer.
Open your browser to the URL given at the bottom of the output and you'll be able to use your site.

# Generate your site
When you're ready to generate HTML files for your site, you should go through
all of the content and remove the `draft` flag.
Then run the following command:

    $ hugo

                    | EN
    +------------------+----+
    Pages            | 12
    Paginator pages  |  0
    Non-page files   |  0
    Static files     |  1
    Processed images |  0
    Aliases          |  0
    Sitemaps         |  1
    Cleaned          |  0

    Total in 9 ms
    $ ll public
    total 24
    drwxr-xr-x   8 mdhender  staff   272 Apr 27 16:29 .
    drwxr-xr-x  13 mdhender  staff   442 Apr 27 16:27 ..
    drwxr-xr-x   7 mdhender  staff   238 Apr 27 16:29 articles
    drwxr-xr-x   3 mdhender  staff   102 Apr 27 15:36 css
    -rw-r--r--   1 mdhender  staff  1764 Apr 27 16:29 index.html
    -rw-r--r--   1 mdhender  staff  2613 Apr 27 16:29 index.xml
    drwxr-xr-x   7 mdhender  staff   238 Apr 27 16:29 posts
    -rw-r--r--   1 mdhender  staff  1320 Apr 27 16:29 sitemap.xml

Now you can copy the contents of the `public/` folder up to your web server for others to use.