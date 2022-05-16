---
datetime: null
description: Docs for create_covers
long_description: 'None None ???  ???  None None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706891
path: create_covers.md
slug: markata/plugins/create_covers
status: published
title: create_covers.py
today: 2022-05-16
---

---

## get_font `function`

None

??? "get_font source"
    ``` python
    def get_font(
        path: Path, draw: ImageDraw.Draw, title: str, size: int = 250
    ) -> ImageFont.FreeTypeFont:
        font = ImageFont.truetype(path, size=size)
        if draw.textsize(title, font=font)[0] > 800:
            return get_font(path, draw, title, size - 10)
        return font
    ```


---

## make_cover `function`

None

??? "make_cover source"
    ``` python
    def make_cover(
        title: str, color: str, output_path: Path, template_path: Path, font_path: Path
    ) -> None:
        image = Image.open(template_path)

        draw = ImageDraw.Draw(image)

        font = get_font(font_path, draw, title)

        color = "rgb(255,255,255)"
        padding = (200, 100)
        bounding_box = [padding[0], padding[1], 1000 - padding[0], 420 - padding[1]]
        x1, y1, x2, y2 = bounding_box
        w, h = draw.textsize(title, font=font)
        x = (x2 - x1 - w) / 2 + x1
        y = (y2 - y1 - h) / 2 + y1
        draw.text((x, y), title, fill=color, font=font, align="center")
        image.save(output_path)
    ```


---

## save `function`

None

??? "save source"
    ``` python
    def save(markata: "Markata") -> None:
        for article in markata.articles:
            output_path = Path(markata.output_dir) / (
                Path(article.metadata["path"]).stem + ".png"
            )

            make_cover(
                article.metadata["title"],
                markata.config["cover_font_color"],
                output_path,
                markata.config["cover_template"],
                markata.config["cover_font"],
            )
    ```