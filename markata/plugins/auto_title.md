---
datetime: null
description: Docs for auto_title
long_description: 'None None ???  ??? '
now: 2022-05-16 15:15:57.706961
path: auto_title.md
slug: markata/plugins/auto_title
status: published
title: auto_title.py
today: 2022-05-16
---

---

## pre_render `function`

None

??? "pre_render source"
    ``` python
    def pre_render(markata) -> None:
        for article in markata.filter('title==""'):
            article["title"] = (
                Path(article["path"]).stem.replace("-", " ").replace("_", " ").title()
            )
    ```