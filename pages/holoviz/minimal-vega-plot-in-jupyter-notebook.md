---
title: A minimal vega plot in jupyter notebook
keywords: holoviz
sidebar: holoviz_sidebar
toc: false
permalink: holoviz-minimal-vega-plot-in-jupyter-notebook.html
folder: holoviz
series: holoviz-series
weight: 2
---
As a proof-of-principle, let's recreate the very first plot we made in the VegaLite tutorial: the simple barchart.

<div id="vis1"></div>
<script type="text/javascript">
    var yourVlSpec = {
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
  };
  vegaEmbed('#vis1', yourVlSpec);
</script>

### Loading the necessary libraries
First things first: loading the necessary libraries. Make sure that these are installed first (see the previous step).

```python
from vega import Vega
```

At this point we won't need `panel` and/or `param` yet.

### Creating the specification
We'll just put the whole specification in a variable that we call `spec`.

```python
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
```

### Drawing the visualisation
And finally we call the `Vega()` function, passing it the `spec` as an argument.

```python
Vega(spec)
```

This will give you the actual plot.
<div id="vis2"></div>
<script type="text/javascript">
    var yourVlSpec = {
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
  };
  vegaEmbed('#vis2', yourVlSpec);
</script>


{% include custom/series_holoviz_next.html %}
