---
title: Tooltips
keywords: vegalite
sidebar: vegalite_sidebar
permalink: vegalite-tooltips.html
folder: vega-lite
series: vegalite-series
weight: 8
---
The easiest - but still very useful - interaction you can create for a plot is to show a tooltip on hover. This is straightforward, but just adding the `tooltip` key in the `encoding` section:

```json
{
  "title": "Showing a tooltip on hover",
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  "mark": "point",
  "encoding": {
    "x": {"field": "Acceleration", "type": "quantitative"},
    "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
    "color": {"field": "Origin", "type": "nominal"},
    "tooltip": [
      {"field": "Acceleration", "type": "quantitative"},
      {"field": "Year", "type": "nominal"}
    ]
  }
}
```

This will get you the following behaviour (interactive):

<div id="vis2"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "title": "Showing a tooltip on hover",
    "data": {
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
    },
    "mark": "point",
    "encoding": {
      "x": {"field": "Acceleration", "type": "quantitative"},
      "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
      "color": {"field": "Origin", "type": "nominal"},
      "tooltip": [
        {"field": "Acceleration", "type": "quantitative"},
        {"field": "Year", "type": "nominal"}
      ]
    }
  };
  vegaEmbed('#vis2', yourVlSpec);
</script>
<!--
<img src="{{ site.baseurl }}/assets/vegalite-tooltip.png" width="50%"/>
-->

{:.exercise}
**Exercise** - Adapt the facetted plot you created before to include a tooltip showing the name of the car, like in the next plot.

<img src="{{ site.baseurl }}/assets/vegalite-tooltip-facetted.png"/>

{% include custom/series_vegalite_next.html %}
