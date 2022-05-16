---
content: ''
cover: ''
datetime: null
description: There are several ways to create your home/landing page, lets walk through
  them.
long_description: There are several ways to create your home/landing page, lets walk
  through There are several ways to create your home/landing page, lets walk through
  By default if there is no index page, the  By default if there is no index page,
  the  You can also h
now: 2022-05-16 15:15:57.706786
path: docs/home-page.md
slug: home-page
status: draft
tags: []
templateKey: ''
title: Creating your Home Page
today: 2022-05-16
---

There are several ways to create your home/landing page, lets walk through
them.

## Default Behavior
_feed_

By default if there is no index page, the [feed
plugin](/markata/plugins/feeds/) will make a home page for you that simply
lists all the the articles by title.

## index.md
_markdown_

You can also have an `index.md` in your pages directory, and it will become the
`index.html` on at render time.  This is how [markata.dev](https://markata.dev)
achieves it's own home page.

## static/index.html
_html_

If you want something more complicated (i.e. not easily done in markdown), you
can simply just make an `index.html` in your `Markata().config['assets_dir']`
and it will become your home page. 

!!! note
    your default `assets_dir` will be the static diretory in the root of your
    project.  You can change this by adding to your `markata.toml` settings
    file.

    ```toml
    [markata]
    assets_dir = "assets"
    ```

This is how the homepage of [waylonwalker.com](https://waylonwalker.com) is achieved.