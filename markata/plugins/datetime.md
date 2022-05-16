---
datetime: null
description: Docs for datetime
long_description: 'Default datetime plugin Default datetime plugin None None ???  ??? '
now: 2022-05-16 15:15:57.706887
path: datetime.md
slug: markata/plugins/datetime
status: published
title: datetime.py
today: 2022-05-16
---

Default datetime plugin


---

## load `function`

None

??? "load source"
    ``` python
    def load(markata: "Markata") -> None:
        for article in markata.iter_articles("datetime"):

            try:
                date = article.metadata["date"]
            except KeyError:
                date = None
            if isinstance(date, str):
                date = dateutil.parser.parse(date)
            if isinstance(date, datetime.date):
                date = datetime.datetime(
                    year=date.year,
                    month=date.month,
                    day=date.day,
                    tzinfo=pytz.utc,
                )

            article["today"] = datetime.date.today()
            article["now"] = datetime.datetime.now()
            article["datetime"] = date
            if date is not None:
                article["date"] = date.date()
    ```