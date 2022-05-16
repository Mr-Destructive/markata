---
datetime: null
description: Docs for cli
long_description: 'Define the layout. Define the layout. ???  ???  None None ???  ???  None
  None ???  ???  None None ???  ???  None None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706869
path: cli.md
slug: markata/cli/cli
status: published
title: cli.py
today: 2022-05-16
---

---

## make_layout `function`

Define the layout.

??? "make_layout source"
    ``` python
    def make_layout() -> Layout:
        """Define the layout."""
        layout = Layout(name="root")

        layout.split(
            Layout(name="header", size=3),
            Layout(name="main"),
        )
        layout["main"].split_row(
            Layout(name="side", ratio=50),
            Layout(name="mid", ratio=30),
            Layout(name="describe", ratio=20),
        )
        layout["mid"].split(
            Layout(name="server"),
            Layout(name="runner"),
        )
        layout["side"].split(
            Layout(name="plugins"),
        )
        return layout
    ```


---

## run_until_keyboard_interrupt `function`

None

??? "run_until_keyboard_interrupt source"
    ``` python
    def run_until_keyboard_interrupt() -> None:
        try:
            while True:
                time.sleep(0.2)
        except KeyboardInterrupt:
            pass
    ```


---

## version_callback `function`

None

??? "version_callback source"
    ``` python
    def version_callback(value: bool) -> None:
        if value:
            from markata import __version__

            typer.echo(f"Markata CLI Version: {__version__}")
            raise typer.Exit()
    ```


---

## json_callback `function`

None

??? "json_callback source"
    ``` python
    def json_callback(value: bool) -> None:
        if value:
            from markata import Markata

            typer.echo(Markata().to_json())
            raise typer.Exit()
    ```


---

## main `function`

None

??? "main source"
    ``` python
    def main(
        version: bool = typer.Option(
            None, "--version", callback=version_callback, is_eager=True
        ),
        to_json: bool = typer.Option(
            None, "--to-json", callback=json_callback, is_eager=True
        ),
    ) -> None:
        # Do other global stuff, handle other global options here
        return
    ```


---

## cli `function`

None

??? "cli source"
    ``` python
    def cli() -> None:
        from markata import Markata

        m = Markata()
        m._pm.hook.cli(markata=m, app=app)
        app()
    ```