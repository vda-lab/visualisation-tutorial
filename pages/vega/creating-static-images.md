---
title: A simple scatterplot
keywords: vega
sidebar: vega_sidebar
permalink: vega-simple-scatterplot.html
folder: vega
series: vega-series
weight: 1
---
Here's the specification for the barest of scatterplots:

```json
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "width": 400,
  "height": 200,
  "padding": 5,

  "data": [
    {
      "name": "table",
      "values": [
        {"x": 15, "y": 8},
        {"x": 72, "y": 25},
        {"x": 35, "y": 44},
        {"x": 44, "y": 29}
      ]
    }
  ],

  "scales": [
    {
      "name": "xscale",
      "domain": {"data": "table", "field": "x"},
      "range": "width"
    },
    {
      "name": "yscale",
      "domain": {"data": "table", "field": "y"},
      "range": "height"
    }
  ],

  "marks": [
    {
      "type": "symbol",
      "from": {"data":"table"},
      "encode": {
        "enter": {
          "x": {"scale": "xscale", "field": "x"},
          "y": {"scale": "yscale", "field": "y"}
        }
      }
    }
  ]
}
```

giving you the following plot:

<div id="vis1"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega/v5.json",
    "width": 400,
    "height": 200,
    "padding": 5,

    "data": [
      {
        "name": "table",
        "values": [
          {"x": 15, "y": 8},
          {"x": 72, "y": 25},
          {"x": 35, "y": 44},
          {"x": 44, "y": 29}
        ]
      }
    ],

    "scales": [
      {
        "name": "xscale",
        "domain": {"data": "table", "field": "x"},
        "range": "width"
      },
      {
        "name": "yscale",
        "domain": {"data": "table", "field": "y"},
        "range": "height"
      }
    ],

    "marks": [
      {
        "type": "symbol",
        "from": {"data":"table"},
        "encode": {
          "enter": {
            "x": {"scale": "xscale", "field": "x"},
            "y": {"scale": "yscale", "field": "y"}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis1', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vega-barest-scatterplot.png" width="50%" />
-->

Compared to [vega-lite]({{ site.baseurl }}/2019/12/vegalite), this is obviously much more verbose, and the resulting plot is just a bare collection of points without axes or axis labels. The vega-lite specification would have looked like this:

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "data": {
    "values": [
      {"x": 15, "y": 8},
      {"x": 72, "y": 25},
      {"x": 35, "y": 44},
      {"x": 44, "y": 29}
    ]
  },
  "mark": "circle",
  "encoding": {
    "x": {"field": "x", "type": "quantitative"},
    "y": {"field": "y", "type": "quantitative"}
  }
}
```

resulting in this plot:

<div id="vis2"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
    "data": {
      "values": [
        {"x": 15, "y": 8},
        {"x": 72, "y": 25},
        {"x": 35, "y": 44},
        {"x": 44, "y": 29}
      ]
    },
    "mark": "circle",
    "encoding": {
      "x": {"field": "x", "type": "quantitative"},
      "y": {"field": "y", "type": "quantitative"}
    }
  };
  vegaEmbed('#vis2', yourVlSpec);
</script>
<!--
<img src="{{ site.baseurl }}/assets/vegalite-barest-scatterplot.png" width="300px"/>
-->

What differences do we see in vega?

- `data` takes an _array_ instead of a single object
- The `mark` is a `symbol`. The default symbol is a circle; the circle _mark_ does not exist.
- `encoding` is moved _within_ `marks` (now plural instead of the singular `mark`)
- The encodings include a `scale` for each element.
- There's an `enter` object within `encoding`.
- In the `marks` section we need to specify the data used by name.
- We have to define `scales` that we can use in the encoding.

{% include custom/series_vega_next.html %}
