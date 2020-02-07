---
title: Zooming and panning
keywords: vegalite
sidebar: vegalite_sidebar
permalink: vegalite-zooming-and-panning.html
folder: vega-lite
series: vegalite-series
weight: 10
---
Using the `interval` selection type, we can actually make a plot zoomable and pannable by binding to the scales.

A simple example:

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  "selection": {
    "grid": {
      "type": "interval", "bind": "scales"
    }
  },
  "mark": "point",
  "encoding": {
    "x": {"field": "Horsepower", "type": "quantitative"},
    "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
    "color": { "value": "lightgrey" }
  }
}
```

The `grid` in this specification is - just like in the previous section - nothing more than a name that we give to the selection. It could have been `abcde` as well...

<div id="vis4"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
    "data": {
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
    },
    "selection": {
      "grid": {
        "type": "interval", "bind": "scales"
      }
    },
    "mark": "point",
    "encoding": {
      "x": {"field": "Horsepower", "type": "quantitative"},
      "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
      "color": { "value": "lightgrey" }
    }
  };
  vegaEmbed('#vis4', yourVlSpec);
</script>

{% include custom/series_vegalite_next.html %}
