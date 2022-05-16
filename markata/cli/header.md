---
datetime: null
description: Docs for header
long_description: 'Display header with clock. Display header with clock. ???  ???  None
  None ???  ??? '
now: 2022-05-16 15:15:57.706826
path: header.md
slug: markata/cli/header
status: published
title: header.py
today: 2022-05-16
---

---

## Header `class`

Display header with clock.

??? "Header source"
    ``` python
    class Header:
        """Display header with clock."""

        def __rich__(self) -> Panel:
            grid = Table.grid(expand=True)
            grid.add_column(justify="center", ratio=1)
            grid.add_column(justify="right")
            grid.add_row(
                "[magenta][b]Markata[/b][/] [bright_black]Live Server[/]",
                datetime.now().ctime(),
            )
            return Panel(grid, style="yellow")
    ```


---

## __rich__ `method`

None

??? "__rich__ source"
    ``` python
    def __rich__(self) -> Panel:
            grid = Table.grid(expand=True)
            grid.add_column(justify="center", ratio=1)
            grid.add_column(justify="right")
            grid.add_row(
                "[magenta][b]Markata[/b][/] [bright_black]Live Server[/]",
                datetime.now().ctime(),
            )
            return Panel(grid, style="yellow")
    ```