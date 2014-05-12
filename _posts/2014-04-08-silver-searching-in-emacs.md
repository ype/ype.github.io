---
title: Silver Searching in Emacs
quote: Using ag in Emacs to Get Stuff Done, FAST!
author: Anton Strilchuk
created: 04-08-2014
status: Completed
comments: true
format: org
isonum: 424
layout: post
kind: article
tags:
-   ag
-   silver-searcher
-   emacs
keywords:
- emacs
- linux
- keyboard shortcut
- os x
- emacs lisp
image: /media/2014-04-08-silver-searching-in-emacs/cover.jpg
video: false
---

<span class="dropcap">I</span> always seem to run into the constant
problem of having to change multiple variables, symbols, function
names, and other usually mundane parts of my code on a regular
basis. Most likely due to the fact that I first name everything in a
random, train of thought manner, only realising later that a more
useful, explanatory definition is required.

Up until last night I found myself opening and closing multiple files
after spending a few minutes in each finding and replacing keywords,
and then ultimately running my code to find out I missed a few in this
file, and a few in that file.

Take for example two files - one named foobar, and the other named
foofoo. In both foobar and foofoo I have a something with the keywords
foofunct. Now this something (variable, function, whatever) needs to
have the same name in both these files. So I decided while editing
the first file foobar that I want to change foofunct to foodef. With
the change made to foobar lock in place and saved, I attempt to run my
code, ultimately to be greeted by the wonderful world of errors saying
something of the sort &ldquo;your doing it wrong, I can&rsquo;t find your flipping
foofunct in foofoo anymore because it&rsquo;s not in foobar&rdquo;

Now this is an ongoing problem I&rsquo;ve had and have always thought there
has to be a better way&#x2026;

# Well maybe I'm just ignorant

Enter &ldquo;The Silver Searcher&rdquo; or &ldquo;ag&rdquo; for sort. Ag is a wonderful
command line tool that lets you quickly search a code file, or set of
files, to find a specific keyword within those file. Ag from the
command line is awesome, but Ag in Emacs is amazing. By adding a few
simple lines to my dotemacs file I am not able to find, replace, and
view a single keyword across multiple files within a matter of
seconds.

# Adding Ag to Emacs (the code bit)

First you are going to have to make sure you have ag installed.

On Mac you can do this through homebrew very easily (if you don&rsquo;t have
homebrew installed already, join the future and install it)

1. Homebrew

        $ brew install the_silver_searcher

2. Macports

        $ port install the_silver_searcher

3. Linux (Debian/Ubuntu)

        $ apt-get install silversearcher-ag

*note: substitute `apt-get` for whichever package manager you use regularly*

## In your dotemacs

In your dotemacs you&rsquo;re going to need a few things. (make sure to use
M-x package-install to get the required packages (ag) (wgrep))

```lisp
(when (executable-find "ag")
  (require 'ag)
  (require 'wgrep-ag)
  (setq-default ag-highlight-search t)
  (global-set-key (kbd "H-q") 'ag-project)
  (global-set-key (kbd "H-z") 'projectile-ag))
```

As you might noticed I am using Hyper-q (H-q) and Hyper-z (H-z) as
hot keys for ag-\*(whatever), you can change these to suit your
preferred keybinding style.

A few other useful keybindings you may want to check out are C-x C-p,
this makes the search buffer writable and lets you edit results
inline. Also, C-c C-f, which activates {next-error-follow-minor-mode} -
which is a nifty feature that quickly shuttles you to the file for the
result your cursor is currently over.

Here&rsquo;s a little demo of how I&rsquo;m using it with my project, Accent, a
music live coding environment for the web.

# In (somewhat of a haphazard) Conclusion

With the setup complete you can now move you cursor over any variable,
function name, definition, word, whatever and run ag on it to find all
the uses of it in either a project, file, or if you&rsquo;re feel
ambitious your entire system (be warned, this sucks the life out of
everything and may take a billion years to complete)
