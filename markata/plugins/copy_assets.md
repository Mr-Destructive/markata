---
datetime: null
description: Docs for copy_assets
long_description: 'None None ???  ??? '
now: 2022-05-16 15:15:57.706904
path: copy_assets.md
slug: markata/plugins/copy_assets
status: published
title: copy_assets.py
today: 2022-05-16
---

---

## save `function`

None

??? "save source"
    ``` python
    def save(markata: "Markata") -> None:
        try:
            output_dir = Path(str(markata.config["output_dir"]))
            assets_dir = Path(str(markata.config["assets_dir"]))
        except KeyError:
            return

        with markata.console.status("copying assets", spinner="aesthetic", speed=0.2):
            if assets_dir.exists():
                shutil.copytree(assets_dir, output_dir, dirs_exist_ok=True)
    ```