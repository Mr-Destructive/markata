---
datetime: null
description: Docs for flat_slug
long_description: 'Flat Slug Plugin Flat Slug Plugin Creates a slug in article.metadata
  if missing based on filename. Creates a slug in article.metadata if missing based
  on filename. None None ???  ??? '
now: 2022-05-16 15:15:57.706929
path: flat_slug.md
slug: markata/plugins/flat_slug
status: published
title: flat_slug.py
today: 2022-05-16
---

Flat Slug Plugin

Creates a slug in article.metadata if missing based on filename.


---

## pre_render `function`

None

??? "pre_render source"
    ``` python
    def pre_render(markata: "Markata") -> None:
        for article in markata.iter_articles(description="creating slugs"):
            try:
                article["slug"] = article.metadata["slug"]
            except KeyError:
                article["slug"] = Path(article["path"]).stem
    ```