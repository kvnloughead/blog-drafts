---
title: 'Command Line Notes'
excerpt: 'A DIY markdown note taking app.'
coverImage: ''
date: '2021-12-03'
author:
  name: Kevin Loughead
  picture: ''
ogImage:
  url: ''
---

I've never been a very good note taker, but I've always appreciated the art. When I got my undergraduate degree in math I tried to be studious. I produced massive quantities of notes in Microsoft OneNote. I suppose they were helpful in a way, etching the concepts in my brain. But ultimately the practice was usustainable, and I've haven't referred to the notes since. 

After graduating I started learning to program. Part of this process was learning how to quickly find relevant information ~~on StackOverflow~~ in the documentation. Who needs notes! But some pieces of information are harder to find then others, and some pieces of information are harder to internalize, so I still needed to take notes sometimes, and I could never find a note taking app that satisfied me completely. So I decided to make one myself. It still doesn't satisfy me completely, but it works and I like it and I keep making it better. Here is an intro to the app.

### Command Line Notes (cln)

(Command Line Notes)[https://github.com/kvnloughead/command-line-notes] is minimal Markdown notetaking app, written in Python. It's primary function is allowing rapid fire opening of Markdown note files, that you can edit in the comfort of your preferred text editor. It collects your notes on your local file system, provides commands allowing you to organize and search through your notes, and even has some basic GitHub integration built in. 

#### Creating and Editing Notes

You can open a note for editing with

```plain-text
$ cln edit git-rebase
```

This will open a file called `~/.notes/default/git-rebase.md` in your preferred editor.[^1] The directory `~/.notes/` will be created the first time you create a note, and the subdirectory `default/` will be created the first time you make a note without explicitly setting a category. Categories can be specified with the `-c | --category` flag. For example, you could keep todo lists for all your different projects:

```plain-text
$ cln edit project-x -c todo 
```

The note file will have some YAML metadata at the top, most of which I'm not doing much with at the moment. 

```yaml
---  
Title: project-x  
Category: todo  
Author: Kevin Loughead  
Date: 2021-12-03  
Tags:   
---  
```

And now you can take your notes and close the file. You can reopen the file at any time using the same command:

```plain-text
$ cln edit project-x -c todo 
```

But maybe you don't always want to open VSCode to take a look at a note file. Often I like to pop open a note for quick review or revising right in my terminal. Well, there's a flag for that:

```plain-text
cln edit git-rebase -e nano  # opens note in nano
```

#### Managing Notes

Changing the metadata of a note is easily accomplished via the `edit` subcommand. You can delete notes easily with `cln delete foo`.[^2] Make sure to specify the category, if it is not the default. You can also the access the entire notes directory with `cln opendir`. This is a feature I felt was lacking in other note taking apps I've tried, and my idea is that it would allow you to more easily organize your notes, although to be honest I have rarely used this feature outside of development.

For a quicker view of the contents of your notes directory, run `cln show`. Currently this prints a simple list of note names, subdivided by category[^3]:

```plain-text

Category -- default
===================
git-rebase.md

Category -- todo
================
project-x.md

```

And I've recently begun to write some subcommands to handle searching through your notes: 

```plain-text
$ cln find substring 
```

which prints a list of notes containing `substring`[^4], and

```plain-text
$ cln grep pattern
```

which basically just runs 

```plain-text
$ grep -r --color --exclude-dir=.git {args.pattern} {BASE_PATH}
```

in your notes folder. It prints a list of the form `<path/to/note>:<line>` for each line in your notes file containing a match for `pattern`.



[^1] Preferred editor can be set in a config file. 
[^2] TODO - implement `-y` flag for "assume yes". By default there is a prompt for confirmation before deletion.
[^3] TODO - add a `--verbose` flag that shows more data for this subcommand.
[^4] TODO - add support for regexes