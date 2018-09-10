# `words`

Because I don't see why I should have to use giants like Hugo or Jekyll if I just want to insert some parsed markdown into simple templates, and sacrifice easy tweaking and fine tuning while I'm at it.

Taking some inspiration from the people over at [suckless](https://suckless.org), this project takes a zero-configuration approach.

- __Want to change the .css of the markdown?__ `$ mv desired.css static/css/markdown.css`
- __Want to insert some custom HTML in every page?__ Go to `templates/item.html` or `front.html` and _do it_.
- __Want to exchange the code parser for some exotic asynchronous one?__ `words.js` is <100 LOC, it'll take you a minute or two at most.

### To get started...

Clone the repository, 
```bash
$ clone https://github.com/LW2904/words.git
```

remove the example posts,

```bash
$ rm -rf content/*
```

and throw your markdown files into `content/`. If you haven't already, add some front-matter ([see below](https://github.com/LW2904/words#front-matter)) and you're good to go.

The "reference implementation" is the `nodejs` flavor, so if speed is not important to you, that's probably the way to go.

`node words.js` will build the page in `public/`, you can do what you will from then on.

- Symlinking public to some folder your web server of choice is hosting
- Making `public/` a submodule pointing to `<NAME>.github.io` (et al)
- ...

If you want to use another implementation consult the READMEs in the relevant folders.

### Folder Structure

```
├── content		# Your markdown files go here
│   │
│   ├── building-a-brainfuck-interpreter.md
│   ├── cheating-in-osu!mania.md
│   ├── ...
│   .
│
├── public		# The static page will be built to this folder and it is
│ 			# deleted and recreated in every run
│
├── static		# This folder and all of its contents will be copied to
│   │			# public/static on building
│   ├── css
│   │   ├── highlighting.css
│   │   └── markdown.css
│   ├── favicon.png
│   └── js
│       └── utils.js
│
└── templates		# mustache template files that are used to build the site
    │
    ├── front.html	# Template for the "landing page" - you will most likely
    │			# want to edit this
    └── item.html	# ...for the items (aka posts, markdown files, ...)
```

Created with the `tree` utility and minimal post-editing.

### Front matter

I hate it. But until I come up with an alternative to throwing some metadata in front of every file that's processed, you will have to add some JSON at the beginning of an `item` (ergo anything in `content/`) and it will be parsed. This looks something like:

```
{ "name": "Front Matter and other Atrocities", "date": "2018-08-31" }

Your content goes here. Yes, just don't mind the ugly blob at the top. The `name` element will be used as the heading for this item.
```

`date` has to be in the ISO 8601 extended date format. Yeah, I had to look that up too, just format it like in the example above, kay?

### Defaults

The default markdown CSS is in `static/css/markdown.css` and is straight up stolen from [sindresorhus/github-markdown-css](https://github.com/sindresorhus/github-markdown-css). It's the minimal amount of CSS needed to replicate GitHub's markdown look. [marked](https://github.com/markedjs/marked) is used to parse markdown.

