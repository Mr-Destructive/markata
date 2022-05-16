---
datetime: null
description: Docs for to_json
long_description: 'None None ???  ??? '
now: 2022-05-16 15:15:57.706953
path: to_json.md
slug: markata/plugins/to_json
status: published
title: to_json.py
today: 2022-05-16
---

---

## save `function`

None

??? "save source"
    ``` python
    def save(markata: "Markata") -> None:
        output_file = Path(markata.config["output_dir"]) / "markata.json"
        output_file.parent.mkdir(parents=True, exist_ok=True)
        output_file.write_text(json.dumps(markata.to_dict(), default=str))
    ```