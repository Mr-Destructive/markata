---
datetime: null
description: Docs for render_markdown
long_description: 'None None ???  ???  None None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706941
path: render_markdown.md
slug: markata/plugins/render_markdown
status: published
title: render_markdown.py
today: 2022-05-16
---

---

## configure `function`

None

??? "configure source"
    ``` python
    def configure(markata: "MarkataMarkdown") -> None:
        if "markdown_extensions" not in markata.config:
            markdown_extensions = [""]
        if isinstance(markata.config["markdown_extensions"], str):
            markdown_extensions = [markata.config["markdown_extensions"]]
        if isinstance(markata.config["markdown_extensions"], list):
            markdown_extensions = markata.config["markdown_extensions"]
        else:
            raise TypeError("markdown_extensions should be List[str]")

        markata.markdown_extensions = [*DEFAULT_MD_EXTENSIONS, *markdown_extensions]
        markata.md = markdown.Markdown(extensions=markata.markdown_extensions)
    ```


---

## render `function`

None

??? "render source"
    ``` python
    def render(markata: "Markata") -> None:
        config = markata.get_plugin_config(__file__)
        with markata.cache as cache:
            for article in markata.iter_articles("rendering markdown"):
                key = markata.make_hash(
                    "render_markdown",
                    "render",
                    article.content,
                )
                html_from_cache = cache.get(key)
                if html_from_cache is None:
                    html = markata.md.convert(article.content)
                    cache.add(key, html, expire=config["cache_expire"])
                else:
                    html = html_from_cache
                article.html = html
                article.article_html = html
    ```


---

## MarkataMarkdown `class`

None

??? "MarkataMarkdown source"
    ``` python
    class MarkataMarkdown(Markata):
            articles: List = []
            md: markdown.Markdown = markdown.Markdown()
            markdown_extensions: List = []
    ```