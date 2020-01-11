---
title: The simplest barchart
keywords: vegalite
sidebar: vegalite_sidebar
permalink: vegalite-simplest-barchart.html
folder: vega-lite
---
Here's a _very_ simple barchart defined in vega-lite.

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

<!--
<img src="{{site.baseurl}}/assets/vegalite-simplestbarchart.png" width="50%" />
-->

The code to generate it:

```json
{
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

What do we see in this code (called the _specification_ for this plot)? The `"$schema"` key indicates what version of vega-lite (or vega) we are using. Always provide this, but we won't mention it further in this tutorial.

The keys in the example above are `data`, `mark` and `encoding`. On the documentation website, you see these three in the menu on the left of the screen.

- `data`: either lists the data that will be used, or provides a link to an external source
- `mark`: tells us what type of visual we want. In this case, we want bars. These can be `area`, `bar`, `circle`, `line`, `point`, `rect`, `rule`, `square`, `text`, `tick` and `geoshape`.
- `encoding`: links marks to data tells us how to link the data to the marks.
