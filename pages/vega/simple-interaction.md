---
title: Simple interaction
keywords: vega
sidebar: vega_sidebar
permalink: vega-simple-interaction.html
folder: vega
---
You do get some interaction for free with vega, including tooltips, effects on hover, etc.

To add a simple _tooltip_, just add that pragma to the marks, for example:

```json
...
"marks": [
  {
    "type": "symbol",
    "from": {"data":"cars"},
    "encode": {
      "enter": {
        "x": {"scale": "xscale", "field": "Acceleration"},
        "y": {"scale": "yscale", "field": "Miles_per_Gallon"},
        "tooltip": {"field": "Name"}
      }
    }
  }
]
...
```

This will show the name of the car when you hover over a point.

{:.exercise}
**Exercise** - Implement this.

You can change the visual encoding of a mark when hovering over it, using code like this:

```json
...
"marks": [
  {
    "type": "symbol",
    "from": {"data":"cars"},
    "encode": {
      "enter": {
        "x": {"scale": "xscale", "field": "Acceleration"},
        "y": {"scale": "yscale", "field": "Miles_per_Gallon"},
        "tooltip": {"field": "Name"}
      },
      "update": {
        "fill": {"value": "steelblue"},
        "fillOpacity": {"value": 0.3},
        "size": {"value": 100}
      },
      "hover": {
        "fill": {"value": "red"},
        "fillOpacity": {"value": 1},
        "size": {"value": 500}
      }
    }
  }
]
...
```

The result (hover over the datapoints):

<div id="vis3"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega/v5.json",
    "width": 400,
    "height": 200,
    "padding": 5,

    "data": [
      {
        "name": "cars",
        "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
      }
    ],

    "scales": [
      {
        "name": "xscale",
        "domain": {"data": "cars", "field": "Acceleration"},
        "range": "width"
      },
      {
        "name": "yscale",
        "domain": {"data": "cars", "field": "Miles_per_Gallon"},
        "range": "height"
      }
    ],
    "axes": [
      {"orient": "bottom", "scale": "xscale", "grid": true},
      {"orient": "left", "scale": "yscale", "grid": true}
    ],
    "marks": [
      {
        "type": "symbol",
        "from": {"data":"cars"},
        "encode": {
          "enter": {
            "x": {"scale": "xscale", "field": "Acceleration"},
            "y": {"scale": "yscale", "field": "Miles_per_Gallon"},
            "tooltip": {"field": "Name"}
          },
          "update": {
            "fill": {"value": "steelblue"},
            "fillOpacity": {"value": 0.3},
            "size": {"value": 100}
          },
          "hover": {
            "fill": {"value": "red"},
            "fillOpacity": {"value": 1},
            "size": {"value": 500}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis3', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vega-hover.png" width="50%" />
-->

{:.exercise}
**Exercise** - What happens if we don't add the update section?
