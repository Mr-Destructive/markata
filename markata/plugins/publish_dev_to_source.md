---
datetime: null
description: Docs for publish_dev_to_source
long_description: 'None None ???  ???  None None ???  ???  None None ???  ???  None
  None ???  ??? '
now: 2022-05-16 15:15:57.706908
path: publish_dev_to_source.md
slug: markata/plugins/publish_dev_to_source
status: published
title: publish_dev_to_source.py
today: 2022-05-16
---

---

## should_join `function`

None

??? "should_join source"
    ``` python
    def should_join(line):
        if line == "":
            return False
        if line is None:
            return False
        if line[0].isalpha():
            return True
        if line[0].startswith("["):
            return True
        if line[0].startswith("!"):
            return True
        return False
    ```


---

## join_lines `function`

None

??? "join_lines source"
    ``` python
    def join_lines(article):
        lines = article.split("\n")
        line_number = 0
        while line_number + 1 < len(lines):
            line = lines[line_number]
            nextline = lines[line_number + 1]
            if should_join(line) and should_join(nextline):
                lines[line_number] = f"{line} {nextline}"
                lines.pop(line_number + 1)
            else:
                line_number += 1

        return "\n".join(lines)
    ```


---

## post_render `function`

None

??? "post_render source"
    ``` python
    def post_render(markata: "Markata") -> None:
        for post in markata.iter_articles(description="saving source documents"):
            from copy import copy, deepcopy

            article = deepcopy(post)

            before_keys = copy(list(article.keys()))
            for key in before_keys:
                if key not in DEV_TO_FRONTMATTER:
                    del article[key]

            article.content = join_lines(article.content)
            article.content = join_lines(article.content)

            if "canonical_url" not in article:
                article["canonical_url"] = f'{markata.config["url"]}/{post["slug"]}/'

            if "published" not in article:
                article["published"] = True

            if "cover_image" not in article:
                article[
                    "cover_image"
                ] = f"{markata.config['images_url']}/{post['slug']}.png"
            post.dev_to = article
    ```


---

## save `function`

None

??? "save source"
    ``` python
    def save(markata: "Markata") -> None:
        output_dir = Path(str(markata.config["output_dir"]))
        output_dir.mkdir(parents=True, exist_ok=True)
        for post in markata.iter_articles(description="saving source documents"):

            with open(output_dir / Path(post["slug"]) / "dev.md", "w+") as f:
                f.write(frontmatter.dumps(post.dev_to))
    ```