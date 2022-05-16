---
datetime: null
description: Docs for hookspec
long_description: Define hook specs. Define hook specs. Namespace that defines all
  specifications for Load hooks. Namespace that defines all specifications for Load
  hooks. configure -> glob -> load -> render -> save configure -> glob -> load ->
  render -> save ???  ???
now: 2022-05-16 15:15:57.706818
path: hookspec.md
slug: markata/hookspec
status: published
title: hookspec.py
today: 2022-05-16
---

Define hook specs.


---

## MarkataSpecs `class`

Namespace that defines all specifications for Load hooks.

configure -> glob -> load -> render -> save

??? "MarkataSpecs source"
    ``` python
    class MarkataSpecs:
        """
        Namespace that defines all specifications for Load hooks.

        configure -> glob -> load -> render -> save
        """
    ```


---

## generic_lifecycle_method `function`

None

??? "generic_lifecycle_method source"
    ``` python
    def generic_lifecycle_method(
        markata: "Markata",
    ) -> Any:
        ...
    ```


---

## cli_lifecycle_method `function`

A Markata lifecycle methos that includes a typer app used for cli's

??? "cli_lifecycle_method source"
    ``` python
    def cli_lifecycle_method(markata: "Markata", app: "typer.Typer") -> Any:
        "A Markata lifecycle methos that includes a typer app used for cli's"
    ```


---

## register_attr `function`

None

??? "register_attr source"
    ``` python
    def register_attr(*attrs: Any) -> Callable:
        def decorator_register(
            func: Callable,
        ) -> Callable:

            for attr in attrs:
                if attr not in registered_attrs:
                    registered_attrs[attr] = []
                registered_attrs[attr].append(
                    {
                        "func": func,
                        "funcname": func.__code__.co_name,
                        "lifecycle": getattr(LifeCycle, func.__code__.co_name),
                    }
                )

            @functools.wraps(func)
            def wrapper_register(markata: "Markata", *args: Any, **kwargs: Any) -> Any:
                return func(markata, *args, **kwargs)

            return wrapper_register

        return decorator_register
    ```


---

## decorator_register `function`

None

??? "decorator_register source"
    ``` python
    def decorator_register(
            func: Callable,
        ) -> Callable:

            for attr in attrs:
                if attr not in registered_attrs:
                    registered_attrs[attr] = []
                registered_attrs[attr].append(
                    {
                        "func": func,
                        "funcname": func.__code__.co_name,
                        "lifecycle": getattr(LifeCycle, func.__code__.co_name),
                    }
                )

            @functools.wraps(func)
            def wrapper_register(markata: "Markata", *args: Any, **kwargs: Any) -> Any:
                return func(markata, *args, **kwargs)

            return wrapper_register
    ```


---

## wrapper_register `function`

None

??? "wrapper_register source"
    ``` python
    def wrapper_register(markata: "Markata", *args: Any, **kwargs: Any) -> Any:
                return func(markata, *args, **kwargs)
    ```