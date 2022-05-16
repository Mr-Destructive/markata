---
datetime: null
description: Docs for lifecycle
long_description: The LifeCycle is a core component for the internal workings of Markata.  It
  The LifeCycle is a core component for the internal workings of Markata.  It LifeCycle
  currently supports the following steps. LifeCycle currently supports the following
  steps
now: 2022-05-16 15:15:57.706821
path: lifecycle.md
slug: markata/lifecycle
status: published
title: lifecycle.py
today: 2022-05-16
---

The LifeCycle is a core component for the internal workings of Markata.  It
sets fourth the hooks available, the methods to run them on the Markata
instance, and the order they run in.

### Usage

``` python
from markata import Lifecycle

step = Lifecycle.glob
```


---

## LifeCycle `class`

LifeCycle currently supports the following steps.

* configure - load and fix configuration
* glob - find files
* load - load files
* pre_render - clean up files/metadata before render
* render - render content
* post_render - clean up rendered content
* save - store results to disk

??? "LifeCycle source"
    ``` python
    class LifeCycle(Enum):
        """
        LifeCycle currently supports the following steps.

        * configure - load and fix configuration
        * glob - find files
        * load - load files
        * pre_render - clean up files/metadata before render
        * render - render content
        * post_render - clean up rendered content
        * save - store results to disk

        """

        configure = auto()
        glob = auto()
        load = auto()
        pre_render = auto()
        render = auto()
        post_render = auto()
        save = auto()

        def __lt__(self, other: object) -> bool:
            """
            Determine whether other is less than this instance.
            """
            if isinstance(other, LifeCycle):
                return self.value < other.value
            if isinstance(other, int):
                return self.value < other
            return NotImplemented

        def __eq__(self, other: object) -> bool:
            """
            Determine whether other is equal to this instance.
            """
            if isinstance(other, LifeCycle):
                return self.value == other.value
            if isinstance(other, int):
                return self.value == other
            return NotImplemented
    ```


---

## __lt__ `method`

Determine whether other is less than this instance.

??? "__lt__ source"
    ``` python
    def __lt__(self, other: object) -> bool:
            """
            Determine whether other is less than this instance.
            """
            if isinstance(other, LifeCycle):
                return self.value < other.value
            if isinstance(other, int):
                return self.value < other
            return NotImplemented
    ```


---

## __eq__ `method`

Determine whether other is equal to this instance.

??? "__eq__ source"
    ``` python
    def __eq__(self, other: object) -> bool:
            """
            Determine whether other is equal to this instance.
            """
            if isinstance(other, LifeCycle):
                return self.value == other.value
            if isinstance(other, int):
                return self.value == other
            return NotImplemented
    ```