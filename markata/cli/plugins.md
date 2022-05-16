---
datetime: null
description: Docs for plugins
long_description: 'None None ???  ???  None None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706840
path: plugins.md
slug: markata/cli/plugins
status: published
title: plugins.py
today: 2022-05-16
---

---

## Plugins `class`

None

??? "Plugins source"
    ``` python
    class Plugins:
        def __init__(self, markata: "Markata"):
            self.m = markata

        def __rich__(self) -> Panel:
            grid = Table.grid(expand=True)
            grid.add_row(f"[bright_blue]{len(self.m._pm.get_plugins())}[/] plugins")
            for plugin in self.m._pm.get_plugins():
                grid.add_row(
                    "".join(
                        [
                            "[bright_black]",
                            ".".join(plugin.__name__.split(".")[:-1]),
                            ".[/]",
                            plugin.__name__.split(".")[-1],
                        ]
                    )
                )
            return Panel(grid, title="plugins", border_style="gold1")
    ```


---

## __init__ `method`

None

??? "__init__ source"
    ``` python
    def __init__(self, markata: "Markata"):
            self.m = markata
    ```


---

## __rich__ `method`

None

??? "__rich__ source"
    ``` python
    def __rich__(self) -> Panel:
            grid = Table.grid(expand=True)
            grid.add_row(f"[bright_blue]{len(self.m._pm.get_plugins())}[/] plugins")
            for plugin in self.m._pm.get_plugins():
                grid.add_row(
                    "".join(
                        [
                            "[bright_black]",
                            ".".join(plugin.__name__.split(".")[:-1]),
                            ".[/]",
                            plugin.__name__.split(".")[-1],
                        ]
                    )
                )
            return Panel(grid, title="plugins", border_style="gold1")
    ```