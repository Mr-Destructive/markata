---
datetime: null
description: Docs for server
long_description: 'Find a port not in ues starting at given port Find a port not in
  ues starting at given port ???  ???  None None ???  ???  None None ???  ???  None
  None ???  ???  None None ???  ???  None None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706878
path: server.md
slug: markata/cli/server
status: published
title: server.py
today: 2022-05-16
---

---

## find_port `function`

Find a port not in ues starting at given port

??? "find_port source"
    ``` python
    def find_port(port: int = 8000) -> int:
        """Find a port not in ues starting at given port"""
        import socket

        with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
            if s.connect_ex(("localhost", port)) == 0:
                return find_port(port=port + 1)
            else:
                return port
    ```


---

## Server `class`

None

??? "Server source"
    ``` python
    class Server:
        def __init__(
            self,
            auto_restart: bool = True,
            directory: Union[str, "Path"] = None,
            port: int = 8000,
        ):
            if directory is None:
                from markata import Markata

                m = Markata()
                directory = Path(str(m.config["output_dir"]))

            self.auto_restart = auto_restart
            self.directory = directory
            self.port = find_port(port=port)
            self.start_server()
            atexit.register(self.kill)

        def start_server(self) -> None:
            import subprocess

            self.cmd = [
                "python",
                "-m",
                "http.server",
                str(self.port),
                "--directory",
                self.directory,
            ]

            self.proc = subprocess.Popen(
                self.cmd,
                stderr=subprocess.PIPE,
                stdout=subprocess.PIPE,
            )
            self.start_time = time.time()

        @property
        def uptime(self) -> int:
            return round(time.time() - self.start_time)

        def kill(self) -> None:
            self.auto_restart = False
            self.proc.kill()

        def __rich__(self) -> Panel:
            if not self.proc.poll():
                return Panel(
                    f"[green]serving on port: [gold1]{self.port} [green]using pid: [gold1]{self.proc.pid} [green]uptime: [gold1]{self.uptime} [green]link: [gold1] http://localhost:{self.port}[/]",
                    border_style="blue",
                    title="server",
                )

            else:

                return Panel(f"[red]server died", title="server", border_style="red")
    ```


---

## __init__ `method`

None

??? "__init__ source"
    ``` python
    def __init__(
            self,
            auto_restart: bool = True,
            directory: Union[str, "Path"] = None,
            port: int = 8000,
        ):
            if directory is None:
                from markata import Markata

                m = Markata()
                directory = Path(str(m.config["output_dir"]))

            self.auto_restart = auto_restart
            self.directory = directory
            self.port = find_port(port=port)
            self.start_server()
            atexit.register(self.kill)
    ```


---

## start_server `method`

None

??? "start_server source"
    ``` python
    def start_server(self) -> None:
            import subprocess

            self.cmd = [
                "python",
                "-m",
                "http.server",
                str(self.port),
                "--directory",
                self.directory,
            ]

            self.proc = subprocess.Popen(
                self.cmd,
                stderr=subprocess.PIPE,
                stdout=subprocess.PIPE,
            )
            self.start_time = time.time()
    ```


---

## uptime `method`

None

??? "uptime source"
    ``` python
    def uptime(self) -> int:
            return round(time.time() - self.start_time)
    ```


---

## kill `method`

None

??? "kill source"
    ``` python
    def kill(self) -> None:
            self.auto_restart = False
            self.proc.kill()
    ```


---

## __rich__ `method`

None

??? "__rich__ source"
    ``` python
    def __rich__(self) -> Panel:
            if not self.proc.poll():
                return Panel(
                    f"[green]serving on port: [gold1]{self.port} [green]using pid: [gold1]{self.proc.pid} [green]uptime: [gold1]{self.uptime} [green]link: [gold1] http://localhost:{self.port}[/]",
                    border_style="blue",
                    title="server",
                )

            else:

                return Panel(f"[red]server died", title="server", border_style="red")
    ```