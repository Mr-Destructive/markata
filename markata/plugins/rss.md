---
datetime: null
description: Docs for rss
long_description: 'Default glob plugin Default glob plugin None None ???  ???  None
  None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706933
path: rss.md
slug: markata/plugins/rss
status: published
title: rss.py
today: 2022-05-16
---

Default glob plugin


---

## render `function`

None

??? "render source"
    ``` python
    def render(markata: "MarkataRss") -> None:
        fg = FeedGenerator()
        url = markata.get_config("url") or ""
        title = markata.get_config("title") or "rss_feed"
        name = markata.get_config("author_name") or ""
        email = markata.get_config("author_email") or ""
        icon = markata.get_config("icon") or ""
        lang = markata.get_config("lang") or ""
        rss_description = markata.get_config("rss_description") or "rss_feed"

        fg.id(url + "/rss.xml")
        fg.title(title)
        fg.author(
            {
                "name": name,
                "email": email,
            }
        )
        fg.link(href=url, rel="alternate")
        fg.logo(icon)
        fg.subtitle(rss_description)
        fg.link(href=url + "/rss.xml", rel="self")
        fg.language(lang)

        try:
            all_posts = reversed(sorted(markata.articles, key=lambda x: x["date"]))
            posts = [post for post in all_posts if post["status"] == "published"]
        except BaseException:
            posts = markata.articles

        for article in posts:
            fe = fg.add_entry()
            fe.id(url + "/" + article["slug"])
            fe.title(article.metadata["title"])
            fe.published(article.metadata["datetime"])
            fe.description(article.metadata["description"])
            fe.summary(article.metadata["long_description"])
            fe.link(href=url + "/" + article["slug"])
            fe.content(article.article_html.translate(dict.fromkeys(range(32))))

        markata.fg = fg
        markata.rss = fg.rss_str(pretty=True)
    ```


---

## save `function`

None

??? "save source"
    ``` python
    def save(markata: "MarkataRss") -> None:
        output_dir = Path(markata.config["output_dir"])
        markata.fg.rss_file(str(output_dir / "rss.xml"))
    ```


---

## MarkataRss `class`

None

??? "MarkataRss source"
    ``` python
    class MarkataRss(Markata):
            fg: "FeedGenerator"
            rss: str
    ```