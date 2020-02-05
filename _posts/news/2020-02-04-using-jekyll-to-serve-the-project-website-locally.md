---
layout: post
author: Graham Higgins
category: project
title:  Using Jekyll to run a local copy of the project website
tags: post project
excerpt: A description of how to use Jekyll to serve this website on http://localhost:4000 
---

## Introduction

The project has taken advantage of Github’s offer of free hosting of project web sites. The trade-off comes in having to deal with the relative complexity of the enabling technology: git and Jekyll. There are four main tasks: acquiring some limited fluency with git, negotiating the installation of Jekyll and its attendant dependencies (Ruby and ruby gems), understanding Jekyll’s basic functioning as a site builder and the prescribed site architecture and finally, acquiring some basic familarity with the Markdown syntax in which the content is expressed.

An expanded version of the Github document [Testing your GitHub Pages site locally with Jekyll](https://help.github.com/en/github/working-with-github-pages/testing-your-github-pages-site-locally-with-jekyll), specialised to the Prime Gap List project’s GitHub Pages site.

[Jekyll](https://jekyllrb.com) is a static site generator with built-in support for GitHub Pages web sites. It was used to create the Prime Gap List project’s [GitHub Pages web site](https://primegap-list-project.github.io/). You can build your own copy of the Prime Gap List project’s GitHub Pages site locally in order to preview and test _your_ changes to the project Github Pages web site.

## Preparation

In order to build locally, some preparation is necessary. You will need to install Jekyll so that it can regenerate the site after you have made changes and also so it can serve the site from `http://localhost:4000`, allowing you to view the rebuilt site. Jekyll is an application written in Ruby, so you will also need to install Ruby - fortunately, this all is covered in the Jekyll documentation.

The Jekyll web site provides comprehensive documentation on installing Jekyll (and Ruby) on a variety of systems. First, check the [Requirements](https://jekyllrb.com/docs/installation/#requirements) to ensure that you’re at least in the ball park.

Then follow the process for your own system  ...

- [Windows](https://jekyllrb.com/docs/installation/windows/).

- [Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/)

- [Other Linux distros](https://jekyllrb.com/docs/installation/other-linux)

- [MacOS](https://jekyllrb.com/docs/installation/macos/)

(Note there are special instructions for [Github Pages on Windows](https://jekyllrb.com/docs/github-pages/))

## Building and viewing the Prime Gap List project’s GitHub Pages site

Once you have installed Jekyll and checked that it runs with `jekyll -v` (or, depending on circumstance, with `bundle exec jekyll -v`).

(_NB. I hate Ruby and its lousy gem package handler but it’s unavoidable if we want to take advantage of free Github Pages hosting, sigh_)

Locally clone the website repository (either your own fork on github or the project’s repository) into (a less unwieldy) `primegap-list-project` folder:

    git clone https://github.com/primegap-list-project/primegap-list-project.github.io.git primegap-list-project 

Then navigate to `primegap-list-project` and run `bundle install` to get all the required Ruby enabling packages.

Now you're just about ready to roll. Firstly ypu need to build the site from the sources:

    bundle exec jekyll build

Now the site is built (basically, the easy-to-write Markdown source is rendered into proper HTML, saving a lot of fuss) and you'll want to view iit.

Handily, the following magic incantation will not only serve the built site on `http://localhost:4000` but will also trigger a “watcher” to make incremental builds whenever you make changes to the content and, as an added bonus, it publishes any draft posts in `_drafts`.

    bundle exec jekyll serve -w -I --drafts

(_I usually start my posts in `_drafts` so I can just casually abandon them and switch to making changes to the site content proper, safe in the knowledge that via `.gitignore`, git is locally configured to ignore `_drafts` so any incomplete posts will remain private to my local clone of the repository._)

Now you can point your browser to `http://localhost:4000` where you will see your local copy of the Prime Gap List project Github Pages site.

## Creating new content

I have no suggestions other than to become slightly familiar with the [Jekyll Github Pages documentation](https://jekyllrb.com/docs/github-pages/) and use the existing posts as an example. Just copy, nuke the main content, edit the rubric as appropriate and save in the _mandatory_ filename format of

    YYYY-MM-DD-title-text.md


### Example of rubric

Taken from this very page ...

    ---
    layout: post
    author: Graham Higgins
    category: project
    title:  Using Jekyll to run a local copy of the project website
    tags: post project
    excerpt: A description of how to use Jekyll to serve this website on http://localhost:4000 
    ---

### Example of Markdown content

Taken from this very page to illustrate how to create a hypertext link and a list ...

    The Jekyll web site provides comprehensive documentation on installing Jekyll (and Ruby) on a variety of systems.
    First, check the [Requirements](https://jekyllrb.com/docs/installation/#requirements) to ensure that you’re at
    least in the ball park.

    Then follow the process for your own system  ...

    - [Windows](https://jekyllrb.com/docs/installation/windows/).

    - [Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/)


## Changing the content of the Prime Gap List project Github Pages site.

Make your changes, view and check your changes, commit your changes when you’re ready then push your changes. Probably best to raise a PR unless you want to be bold.


---