---
datetime: null
description: Docs for publish_source
long_description: 'None None ???  ??? '
now: 2022-05-16 15:15:57.706895
path: publish_source.md
slug: markata/plugins/publish_source
status: published
title: publish_source.py
today: 2022-05-16
---

---

## save `function`

None

??? "save source"
    ``` python
    def save(markata: "Markata") -> None:
        output_dir = Path(str(markata.config["output_dir"]))
        output_dir.mkdir(parents=True, exist_ok=True)
        for article in markata.iter_articles(description="saving source documents"):
            with open(
                output_dir / Path(article["slug"]).parent / Path(article["path"]).name, "w+"
            ) as f:
                f.write(frontmatter.dumps(article))
    ```