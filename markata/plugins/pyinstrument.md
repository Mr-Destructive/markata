---
datetime: null
description: Docs for pyinstrument
long_description: Markata plugin to create a pyinstrument profile if pyinstrument
  is installed. Markata plugin to create a pyinstrument profile if pyinstrument is
  installed. The profile will be saved to  The profile will be saved to  None None
  ???  ???  set the should
now: 2022-05-16 15:15:57.706937
path: pyinstrument.md
slug: markata/plugins/pyinstrument
status: published
title: pyinstrument.py
today: 2022-05-16
---

Markata plugin to create a pyinstrument profile if pyinstrument is installed.

The profile will be saved to <output_dir>/_profile/index.html


---

## MarkataInstrument `class`

None

??? "MarkataInstrument source"
    ``` python
    class MarkataInstrument(Markata):
        should_profile = False
        profiler = None
    ```


---

## configure `function`

set the should_profile variable

??? "configure source"
    ``` python
    def configure(markata: MarkataInstrument) -> None:
        "set the should_profile variable"

        if "should_profile" not in markata.__dict__.keys():
            try:
                markata.should_profile = markata.config["pyinstrument"]["should_profile"]
            except KeyError:
                markata.should_profile = False
    ```


---

## glob `function`

start the profiler as soon as possible

??? "glob source"
    ``` python
    def glob(markata: MarkataInstrument) -> None:
        "start the profiler as soon as possible"
        if markata.should_profile:
            try:
                markata.profiler = Profiler()
                markata.profiler.start()
            except NameError:
                "ignore if Profiler does not exist"
                ...
    ```


---

## save `function`

stop the profiler and save as late as possible

??? "save source"
    ``` python
    def save(markata: MarkataInstrument) -> None:
        "stop the profiler and save as late as possible"
        if markata.should_profile:
            try:

                if "profiler" in markata.__dict__.keys():
                    output_file = (
                        Path(markata.config["output_dir"]) / "_profile" / "index.html"
                    )
                    output_file.parent.mkdir(parents=True, exist_ok=True)
                    markata.profiler.stop()
                    html = markata.profiler.output_html()
                    output_file.write_text(html)
                    markata.console.print(markata.profiler.output_text())

            except AttributeError:
                "ignore if markata does not have a profiler attribute"
                ...
    ```