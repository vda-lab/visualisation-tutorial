---
title: Panel and Vega
keywords: holoviz
sidebar: holoviz_sidebar
toc: false
permalink: holoviz-panel-and-vega.html
folder: holoviz
series: holoviz-series
weight: 8
---
So let's finally combine Panel with Vega. As for creating a pane with markdown text or a figure, we can use `pn.pane.Vega()` and give it a specification.


```python
import panel as pn
from vega import Vega
pn.extension('vega')

spec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
    "description": "A simple bar chart with embedded data.",
    "data": {
      "values": [
        {"a": "A", "b": 28},
        {"a": "B", "b": 55},
        {"a": "C", "b": 43},
        {"a": "D", "b": 91}
      ]
    },
    "mark": "bar",
    "encoding": {
      "x": {"field": "b", "type": "quantitative"},
      "y": {"field": "a", "type": "nominal"}
    }
  }
pn.pane.Vega(spec)
```

You'll get

<img src="{{site.baseurl}}/assets/vegalite-simplestbarchart.png" width="50%" />

Now we can combine this with other panes. In the Vega and VegaLite tutorials, we defined the title within the specification itself. Now, instead, we can define it outside:

```python
pn.Column(pn.pane.Markdown("# This is a horizontal barchart"),
          pn.Row(
                 pn.panel("This barchart with 4 categories shows us how we can combine different panes, including vega plots"),
                 pn.pane.Vega(spec)

          ))
```

<img src="{{ site.baseurl }}/assets/holoviz-barchart-in-panel.png" />

Or combining two plots:
```python
pn.Column(pn.pane.Markdown("# This is a horizontal barchart"),
          pn.Row(
                 pn.pane.Vega(spec),
                 pn.pane.Vega(spec)

          ))
```

{% include custom/series_holoviz_next.html %}
