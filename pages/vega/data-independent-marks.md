---
title: Data-independent marks
keywords: vega
sidebar: vega_sidebar
permalink: vega-data-independent-marks.html
folder: vega
series: vega-series
weight: 3
---
In the `marks` section in vega, the `from` pragma points to the dataset that should be used: for every datapoint in the dataset, a single mark is created. If _no_ `from` is provided, vega defaults to creating a single mark. Let's for example add a red square and a bit of text to the plot above:

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
    },
    {
      "type": "rect",
      "encode": {
        "enter": {
          "x": {"value": 50},
          "y": {"value": 50},
          "width": {"value": 30},
          "height": {"value": 30},
          "fill": {"value": "red"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "text": {"value": "This is some text"},
          "x": {"value": 100},
          "y": {"value": 50}
        }
      }
    }
  ]
}
```

Notice that there is no `from` defined for the square and the text.

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
      },
      {
        "type": "rect",
        "encode": {
          "enter": {
            "x": {"value": 50},
            "y": {"value": 50},
            "width": {"value": 30},
            "height": {"value": 30},
            "fill": {"value": "red"}
          }
        }
      },
      {
        "type": "text",
        "encode": {
          "enter": {
            "text": {"value": "This is some text"},
            "x": {"value": 100},
            "y": {"value": 50}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis1', yourVlSpec);
</script>

{% include custom/series_vega_next.html %}
