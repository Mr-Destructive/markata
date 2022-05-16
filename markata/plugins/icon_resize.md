---
datetime: null
description: Docs for icon_resize
long_description: 'Icon Resize Plugin Icon Resize Plugin None None ???  ???  None
  None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706925
path: icon_resize.md
slug: markata/plugins/icon_resize
status: published
title: icon_resize.py
today: 2022-05-16
---

Icon Resize Plugin


---

## render `function`

None

??? "render source"
    ``` python
    def render(markata: "MarkataIcons") -> None:
        if "icon" not in markata.config:
            return
        base_out_file = Path(markata.config["output_dir"]) / markata.config["icon"]

        with Image.open(Path(markata.config["assets_dir"]) / markata.config["icon"]) as img:
            markata.icons = []
            for width in [48, 72, 96, 144, 192, 256, 384, 512]:
                height = int(float(img.size[1]) * float(width / float(img.size[0])))
                filename = Path(
                    f"{base_out_file.stem}_{width}x{height}{base_out_file.suffix}"
                )
                markata.icons.append(
                    {
                        "src": str(filename),
                        "sizes": f"{width}x{width}",
                        "type": f"image/{img.format}".lower(),
                        "purpose": "any maskable",
                    }
                )
    ```


---

## save `function`

None

??? "save source"
    ``` python
    def save(markata: "MarkataIcons") -> None:
        if "icon" not in markata.config:
            return
        base_out_file = Path(markata.config["output_dir"]) / markata.config["icon"]
        for width in [48, 72, 96, 144, 192, 256, 384, 512]:
            with Image.open(
                Path(markata.config["assets_dir"]) / markata.config["icon"]
            ) as img:
                height = int(float(img.size[1]) * float(width / float(img.size[0])))
                img = img.resize((width, height), Image.ANTIALIAS)
                filename = Path(
                    f"{base_out_file.stem}_{width}x{height}{base_out_file.suffix}"
                )
                out_file = Path(markata.config["output_dir"]) / filename
                img.save(out_file)
    ```


---

## MarkataIcons `class`

None

??? "MarkataIcons source"
    ``` python
    class MarkataIcons(Markata):
            icons: List[Dict[str, str]]
    ```