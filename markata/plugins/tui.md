---
datetime: null
description: Docs for tui
long_description: 'None None ???  ???  None None ???  ???  None None ???  ???  None
  None ???  ???  None None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706981
path: tui.md
slug: markata/plugins/tui
status: published
title: tui.py
today: 2022-05-16
---

---

## MarkataWidget `class`

None

??? "MarkataWidget source"
    ``` python
    class MarkataWidget(Widget):
        def __init__(self, markata: Markata, widget: str = "server"):
            super().__init__(widget)
            self.m = markata
            self.widget = widget
            self.renderable = getattr(self.m, self.widget)

        def render(self):
            return self.renderable

        async def update(self, renderable: RenderableType) -> None:
            self.renderable = renderable
            self.refresh()
    ```


---

## MarkataApp `class`

None

??? "MarkataApp source"
    ``` python
    class MarkataApp(App):
        async def on_mount(self) -> None:
            self.m = Markata()
            self.m.console.quiet = True
            self.server = MarkataWidget(self.m, "server")
            self.runner = MarkataWidget(self.m, "runner")
            self.plugins = MarkataWidget(self.m, "plugins")
            self.summary = MarkataWidget(self.m, "summary")
            await self.view.dock(Footer(), edge="bottom")
            await self.view.dock(self.plugins, edge="left", size=30, name="plugins")
            await self.view.dock(self.summary, edge="right", size=30, name="summary")
            await self.view.dock(self.server, self.runner, edge="top")
            self.set_interval(1, self.action_refresh)

        async def on_load(self, event):
            await self.bind("q", "quit", "quit")
            await self.bind("r", "refresh", "refresh")

        async def action_refresh(self) -> None:
            self.refresh()
            self.runner.refresh()
            self.server.refresh()
            self.plugins.refresh()
            self.summary.refresh()
    ```


---

## cli `function`

None

??? "cli source"
    ``` python
    def cli(app, markata):
        @app.command()
        def tui():
            MarkataApp.run(log="textual.log")
    ```


---

## __init__ `method`

None

??? "__init__ source"
    ``` python
    def __init__(self, markata: Markata, widget: str = "server"):
            super().__init__(widget)
            self.m = markata
            self.widget = widget
            self.renderable = getattr(self.m, self.widget)
    ```


---

## render `method`

None

??? "render source"
    ``` python
    def render(self):
            return self.renderable
    ```


---

## tui `function`

None

??? "tui source"
    ``` python
    def tui():
            MarkataApp.run(log="textual.log")
    ```