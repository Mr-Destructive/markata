---
datetime: null
description: Docs for glob
long_description: 'Default glob plugin Default glob plugin None None ???  ??? '
now: 2022-05-16 15:15:57.706973
path: glob.md
slug: markata/plugins/glob
status: published
title: glob.py
today: 2022-05-16
---

Default glob plugin


---

## glob `function`

None

??? "glob source"
    ``` python
    def glob(markata: "Markata") -> None:

        markata.files = list(
            flatten([Path().glob(str(pattern)) for pattern in markata.glob_patterns])
        )
        markata.content_directories = list(set([f.parent for f in markata.files]))

        try:
            ignore = markata.config["glob"]["use_gitignore"] or True
        except KeyError:
            ignore = True

        if ignore and (Path(".gitignore").exists() or Path(".markataignore").exists()):
            import pathspec

            lines = []

            if Path(".gitignore").exists():
                lines.extend(Path(".gitignore").read_text().splitlines())

            if Path(".markataignore").exists():
                lines.extend(Path(".markataignore").read_text().splitlines())

            spec = pathspec.PathSpec.from_lines("gitwildmatch", lines)

            markata.files = [
                file for file in markata.files if not spec.match_file(str(file))
            ]
    ```