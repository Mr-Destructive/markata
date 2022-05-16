---
datetime: null
description: Docs for test_doc_page
long_description: 'None None ???  ???  None None ???  ???  None None ???  ???  None
  None ???  ???  None None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706800
path: test_doc_page.md
slug: tests/test_doc_page
status: published
title: test_doc_page.py
today: 2022-05-16
---

---

## make_project `function`

None

??? "make_project source"
    ``` python
    def make_project(tmp_path_factory: Any) -> Any:
        project = tmp_path_factory.mktemp("project")
        module = project / "my_module.py"
        module.write_text(
            textwrap.dedent(
                """
                '''
                Module level docstring
                '''

                def my_func():
                    '''
                    docstring for my_func
                    '''
                class MyClass:
                    '''
                    docstring for MyClass
                    '''

                    def my_method(self):
                        '''
                        docstring for my_method
                        '''

                """
            )
        )
        markta_toml = project / "markata.toml"
        markta_toml.write_text(
            textwrap.dedent(
                """
                [markata]
                hooks = [
                    "markata.plugins.docs",
                    "default",
                    ]

                """
            )
        )

        return project
    ```


---

## test_loaded `function`

None

??? "test_loaded source"
    ``` python
    def test_loaded(make_project: Any) -> None:
        os.chdir(make_project)
        m = Markata()
        assert len(m.py_files) == 1
    ```


---

## test_run `function`

None

??? "test_run source"
    ``` python
    def test_run(make_project: Any) -> Any:
        os.chdir(make_project)
        m = Markata()
        m.run()
        return make_project
    ```


---

## test_markout_exists `function`

None

??? "test_markout_exists source"
    ``` python
    def test_markout_exists(test_run: Any) -> Any:
        markout = test_run / "markout"
        assert markout.exists()
    ```


---

## test_index_exists `function`

None

??? "test_index_exists source"
    ``` python
    def test_index_exists(test_run: Any) -> Any:
        markout = test_run / "markout"
        index = markout / "index.html"
        assert index.exists()
    ```


---

## test_rss_exists `function`

None

??? "test_rss_exists source"
    ``` python
    def test_rss_exists(test_run: Any) -> Any:
        markout = test_run / "markout"
        rss = markout / "rss.xml"
        assert rss.exists()
    ```