---
title: Interact
keywords: holoviz
sidebar: holoviz_sidebar
toc: false
permalink: holoviz-interact.html
folder: holoviz
series: holoviz-series
weight: 6
---

```python
data = [
    {"a": 1, "b": 5},
    {"a": 10, "b": 55},
    {"a": 100, "b": 255},
    {"a": 2, "b": 555},
    {"a": 20, "b": 5},
    {"a": 200, "b": 52},
    {"a": 3, "b": 254},
    {"a": 30, "b": 257}
]

def select_row(row=0):
    return data[row]

app = pn.interact(select_row, row=(0, len(data)-1))
app
```

{% include custom/series_holoviz_next.html %}
