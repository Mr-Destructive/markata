---
datetime: null
description: Docs for sitemap
long_description: 'None None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706977
path: sitemap.md
slug: markata/plugins/sitemap
status: published
title: sitemap.py
today: 2022-05-16
---

---

## render `function`

None

??? "render source"
    ``` python
    def render(markata: Markata) -> None:
        url = markata.get_config("url") or ""

        sitemap = {
            "urlset": [
                {
                    "url": {
                        "loc": url + "/" + article["slug"] + "/",
                        "changefreq": "daily",
                        "priority": "0.7",
                    }
                }
                for article in markata.articles
                if article["status"] == "published"
            ]
        }

        sitemap = (
            anyconfig.dumps(sitemap, "xml")
            .decode("utf-8")
            .replace(
                "<urlset>",
                '<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9" xmlns:news="http://www.google.com/schemas/sitemap-news/0.9" xmlns:xhtml="http://www.w3.org/1999/xhtml" xmlns:mobile="http://www.google.com/schemas/sitemap-mobile/1.0" xmlns:image="http://www.google.com/schemas/sitemap-image/1.1" xmlns:video="http://www.google.com/schemas/sitemap-video/1.1">',
            )
            .replace("</url>", "</url>\n")
        )
        setattr(markata, "sitemap", sitemap)
    ```


---

## save `function`

None

??? "save source"
    ``` python
    def save(markata: Markata) -> None:
        with open(Path(markata.config["output_dir"]) / "sitemap.xml", "w") as f:
            f.write(markata.sitemap)
    ```