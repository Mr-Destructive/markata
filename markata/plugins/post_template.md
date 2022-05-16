---
datetime: null
description: Docs for post_template
long_description: 'None None ???  ??? '
now: 2022-05-16 15:15:57.706984
path: post_template.md
slug: markata/plugins/post_template
status: published
title: post_template.py
today: 2022-05-16
---

---

## render `function`

None

??? "render source"
    ``` python
    def render(markata: "Markata") -> None:
        if "post_template" in markata.config:
            template_file = markata.config["post_template"]
        else:
            template_file = Path(__file__).parent / "default_post_template.html"
        with open(template_file) as f:
            template = Template(f.read())
        for article in markata.iter_articles("apply template"):

            article.html = template.render(
                body=article.html,
                toc=markata.md.toc,  # type: ignore
                config=markata.config,
                **article,
            )
    ```