---
datetime: null
description: Docs for generator
long_description: 'add generator meta tag add generator meta tag None None ???  ??? '
now: 2022-05-16 15:15:57.706912
path: generator.md
slug: markata/plugins/generator
status: published
title: generator.py
today: 2022-05-16
---

add generator meta tag


---

## render `function`

None

??? "render source"
    ``` python
    def render(markata: Markata) -> None:
        for article in markata.iter_articles("add ssg tag"):
            soup = BeautifulSoup(article.html, features="lxml")
            tag = soup.new_tag("meta")
            tag.attrs["content"] = f"markata {__version__}"
            tag.attrs["name"] = "generator"
            soup.head.append(tag)
            article.soup = soup
            article.html = soup.prettify()
    ```