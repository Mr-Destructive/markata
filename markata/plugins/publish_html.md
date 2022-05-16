---
datetime: null
description: Docs for publish_html
long_description: 'None None ???  ??? '
now: 2022-05-16 15:15:57.706921
path: publish_html.md
slug: markata/plugins/publish_html
status: published
title: publish_html.py
today: 2022-05-16
---

---

## save `function`

None

??? "save source"
    ``` python
    def save(markata: "Markata") -> None:
        output_dir = Path(markata.config["output_dir"])  # type: ignore
        output_dir.mkdir(parents=True, exist_ok=True)

        for article in markata.articles:
            if article["slug"] == "index":
                article_path = output_dir / "index.html"
            else:
                article_path = output_dir / article["slug"] / "index.html"
            article_path.parent.mkdir(parents=True, exist_ok=True)
            with open(article_path, "w+") as f:
                f.write(article.html)
    ```