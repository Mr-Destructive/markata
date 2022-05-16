---
datetime: null
description: Docs for summary
long_description: 'None None ???  ???  None None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706830
path: summary.md
slug: markata/cli/summary
status: published
title: summary.py
today: 2022-05-16
---

---

## Summary `class`

None

??? "Summary source"
    ``` python
    class Summary:
        def __init__(self, m: "Markata", simple: bool = False) -> None:
            self.m = m
            self.simple = simple

        def __rich__(self) -> Union[Panel, Table]:
            grid = Table.grid(expand=True)
            grid.add_row(f"[bright_blue]{len(self.m.articles)}[/] articles")
            grid.add_row(
                f"[green]{len([a for a in self.m.articles if a['status'] =='published'])}[/] published"
            )
            grid.add_row(
                f"[gold1]{len([a for a in self.m.articles if a['status'] =='draft'])}[/] drafts"
            )
            grid.add_row("")
            grid.add_row("[bold gold1]TAGS[/]")
            from collections import Counter

            from more_itertools import flatten

            try:
                for tag, count in Counter(
                    list(flatten([a["tags"] for a in self.m.articles]))
                ).most_common():
                    grid.add_row(f'{count} {" "*(3-len(str(count)))} {tag}')
            except KeyError:
                ...

            try:
                grid.add_row("[bold gold1]Series[/]")
                for series, count in Counter(
                    [a["templateKey"] for a in self.m.articles]
                ).most_common():
                    grid.add_row(f'{count} {" "*(3-len(str(count)))} {series}')
            except KeyError:
                ...
            if self.simple:
                return grid
            else:
                return Panel(grid, title="[gold1]summary[/]", border_style="magenta")
    ```


---

## __init__ `method`

None

??? "__init__ source"
    ``` python
    def __init__(self, m: "Markata", simple: bool = False) -> None:
            self.m = m
            self.simple = simple
    ```


---

## __rich__ `method`

None

??? "__rich__ source"
    ``` python
    def __rich__(self) -> Union[Panel, Table]:
            grid = Table.grid(expand=True)
            grid.add_row(f"[bright_blue]{len(self.m.articles)}[/] articles")
            grid.add_row(
                f"[green]{len([a for a in self.m.articles if a['status'] =='published'])}[/] published"
            )
            grid.add_row(
                f"[gold1]{len([a for a in self.m.articles if a['status'] =='draft'])}[/] drafts"
            )
            grid.add_row("")
            grid.add_row("[bold gold1]TAGS[/]")
            from collections import Counter

            from more_itertools import flatten

            try:
                for tag, count in Counter(
                    list(flatten([a["tags"] for a in self.m.articles]))
                ).most_common():
                    grid.add_row(f'{count} {" "*(3-len(str(count)))} {tag}')
            except KeyError:
                ...

            try:
                grid.add_row("[bold gold1]Series[/]")
                for series, count in Counter(
                    [a["templateKey"] for a in self.m.articles]
                ).most_common():
                    grid.add_row(f'{count} {" "*(3-len(str(count)))} {series}')
            except KeyError:
                ...
            if self.simple:
                return grid
            else:
                return Panel(grid, title="[gold1]summary[/]", border_style="magenta")
    ```