---
title: Axes
keywords: vega
sidebar: vega_sidebar
permalink: vega-axes.html
folder: vega
series: vega-series
weight: 8
---
The current plot is still extremely bare, without any axes. So let's add those. See [https://vega.github.io/vega/docs/axes/](https://vega.github.io/vega/docs/axes/) for documentation.

To add axes to this plot, we merely add the following just before the `marks` section:

```json
...
"scales": ...,
"axes": [
  {"orient": "bottom", "scale": "xscale"},
  {"orient": "left", "scale": "yscale"}
],
"marks": ...
...
```

This will give you the following:

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
          {"x": 15, "y": 8, "category": "A"},
          {"x": 72, "y": 25, "category": "B"},
          {"x": 35, "y": 44, "category": "C"},
          {"x": 44, "y": 29, "category": "A"},
          {"x": 24, "y": 20, "category": "B"}
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
      },
      {
        "name": "colourScale",
        "type": "ordinal",
        "domain": {"data": "table", "field": "category"},
        "range": {"scheme": "category10"}
      }
    ],
    "axes": [
      {"orient": "bottom", "scale": "xscale"},
      {"orient": "left", "scale": "yscale"}
    ],
    "marks": [
      {
        "type": "symbol",
        "from": {"data":"table"},
        "encode": {
          "enter": {
            "x": {"scale": "xscale", "field": "x"},
            "y": {"scale": "yscale", "field": "y"},
            "size": {"value": 200},
            "fill": {"scale": "colourScale", "field": "category"}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis1', yourVlSpec);
</script>

For axes, you must provide the orientation (whether `top`, `bottom`, `left` or `right`), and the scale that decides where the ticks should come.

{:.exercise}
**Exercise** - Add these axes to the plot you created in the "colour scales" section, but also add axis titles and grid lines.

<!--
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "width": 400,
  "height": 200,
  "padding": 5,

  "data": [
    {
      "name": "table",
      "values": [
        {"x": 15, "y": 8, "category": "A"},
        {"x": 72, "y": 25, "category": "B"},
        {"x": 35, "y": 44, "category": "C"},
        {"x": 44, "y": 29, "category": "A"},
        {"x": 24, "y": 20, "category": "B"}
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
    },
    {
      "name": "colourScale",
      "type": "ordinal",
      "domain": {"data": "table", "field": "category"},
      "range": {"scheme": "category10"}
    }
  ],
  "axes": [
    {"orient": "bottom", "scale": "xscale", "grid": true},
    {"orient": "left", "scale": "yscale", "grid": true}
  ],
  "marks": [
    {
      "type": "symbol",
      "from": {"data":"table"},
      "encode": {
        "enter": {
          "x": {"scale": "xscale", "field": "x"},
          "y": {"scale": "yscale", "field": "y"},
          "size": {"value": 200},
          "fill": {"scale": "colourScale", "field": "category"}
        }
      }
    }
  ]
}
-->

{% include custom/series_vega_next.html %}
