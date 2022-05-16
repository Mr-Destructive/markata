---
datetime: null
description: Docs for runner
long_description: 'Display Footer Display Footer ???  ???  None None ???  ???  None
  None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706844
path: runner.md
slug: markata/cli/runner
status: published
title: runner.py
today: 2022-05-16
---

---

## Runner `class`

Display Footer

??? "Runner source"
    ``` python
    class Runner:
        """Display Footer"""

        _status = "waiting"

        _dirhash = ""
        time = time.time()

        def __init__(self, markata: "Markata") -> None:
            self.m = markata

        def run(self) -> None:
            self.status = "running"
            self.m.run()
            self.time = time.time()
            self.status = "waiting"

        def __rich__(self) -> Panel:

            if self._dirhash != self.m.content_dir_hash:
                self.run()
                self._dirhash = self.m.content_dir_hash

            s = f"runner is waiting {round(time.time() - self.time)}"

            return Panel(Text(s), border_style="green", title="runner")
    ```


---

## __init__ `method`

None

??? "__init__ source"
    ``` python
    def __init__(self, markata: "Markata") -> None:
            self.m = markata
    ```


---

## run `method`

None

??? "run source"
    ``` python
    def run(self) -> None:
            self.status = "running"
            self.m.run()
            self.time = time.time()
            self.status = "waiting"
    ```


---

## __rich__ `method`

None

??? "__rich__ source"
    ``` python
    def __rich__(self) -> Panel:

            if self._dirhash != self.m.content_dir_hash:
                self.run()
                self._dirhash = self.m.content_dir_hash

            s = f"runner is waiting {round(time.time() - self.time)}"

            return Panel(Text(s), border_style="green", title="runner")
    ```