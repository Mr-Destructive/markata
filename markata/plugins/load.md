---
datetime: null
description: Docs for load
long_description: 'Default load plugin. Default load plugin. None None ???  ???  None
  None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706988
path: load.md
slug: markata/plugins/load
status: published
title: load.py
today: 2022-05-16
---

Default load plugin.


---

## load `function`

None

??? "load source"
    ``` python
    def load(markata: "MarkataMarkdown") -> None:
        progress = Progress(
            BarColumn(bar_width=None), transient=True, console=markata.console
        )

        futures = [get_post(article, markata) for article in markata.files]
        task_id = progress.add_task("loading markdown")
        progress.update(task_id, total=len(futures))
        with progress:
            while not all([f.done() for f in futures]):
                time.sleep(0.1)
                progress.update(task_id, total=len([f for f in futures if f.done()]))
        articles = [f.result() for f in futures]
        articles = [a for a in articles if a]
        markata.articles = articles
    ```


---

## get_post `function`

None

??? "get_post source"
    ``` python
    def get_post(path: Path, markata: "Markata") -> Optional[Callable]:
        # -> Optional["Post"]:
        default = {
            "cover": "",
            "title": "",
            "tags": [],
            "status": "draft",
            "templateKey": "",
            "path": str(path),
            "description": "",
            "content": "",
        }
        try:
            post: "Post" = frontmatter.load(path)
            post.metadata = {**default, **post.metadata}
        except ParserError:
            return None
            post = default
        except ValueError:
            return None
            post = default
        post.metadata["path"] = str(path)
        return post
    ```


---

## MarkataMarkdown `class`

None

??? "MarkataMarkdown source"
    ``` python
    class MarkataMarkdown(Markata):
            articles: List = []
    ```