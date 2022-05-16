---
datetime: null
description: Docs for test_one_default_page
long_description: 'None None ???  ???  None None ???  ???  None None ???  ???  None
  None ???  ???  None None ???  ???  None None ???  ??? '
now: 2022-05-16 15:15:57.706796
path: test_one_default_page.md
slug: tests/test_one_default_page
status: published
title: test_one_default_page.py
today: 2022-05-16
---

---

## make_index `function`

None

??? "make_index source"
    ``` python
    def make_index(tmp_path_factory: Any) -> Any:
        fn = tmp_path_factory.mktemp("pages") / "index.md"
        fn.write_text(
            textwrap.dedent(
                """
                ---
                templateKey: blog-post
                tags: ['python',]
                title:  My Awesome Post
                date: 2022-01-21T16:40:34
                status: draft

                ---

                This is my awesome post.
                """
            )
        )
        return tmp_path_factory
    ```


---

## test_loaded `function`

None

??? "test_loaded source"
    ``` python
    def test_loaded(make_index: Any) -> None:
        os.chdir(make_index.getbasetemp())
        m = Markata()
        assert len(m.articles) == 1
    ```


---

## test_run `function`

None

??? "test_run source"
    ``` python
    def test_run(make_index: Any) -> Any:
        os.chdir(make_index.getbasetemp())
        m = Markata()
        m.run()
        return make_index
    ```


---

## test_markout_exists `function`

None

??? "test_markout_exists source"
    ``` python
    def test_markout_exists(test_run: Any) -> Any:
        markout = test_run.getbasetemp() / "markout"
        assert markout.exists()
    ```


---

## test_index_exists `function`

None

??? "test_index_exists source"
    ``` python
    def test_index_exists(test_run: Any) -> Any:
        markout = test_run.getbasetemp() / "markout"
        index = markout / "index.html"
        assert index.exists()
    ```


---

## test_rss_exists `function`

None

??? "test_rss_exists source"
    ``` python
    def test_rss_exists(test_run: Any) -> Any:
        markout = test_run.getbasetemp() / "markout"
        rss = markout / "rss.xml"
        assert rss.exists()
    ```