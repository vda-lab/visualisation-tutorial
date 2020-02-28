---
title: Legends
keywords: vega
sidebar: vega_sidebar
permalink: vega-legends.html
folder: vega
series: vega-series
weight: 9
---
We now have a plot with points in different colours that are dependent upon the category, but we can't tell which colour is which category. Enter legends.

By default, a legend is placed in the top right. In our code above, we set the colour (`fill`) based on the scale `colourScale`. It is this scale that we need to make a legend for:

{% highlight json %}
"legends": [
  {
    "fill": "colourScale"
  }
],
{% endhighlight %}

We used `fill` because it corresponds to the encoding pragma that we need the legend for, and `colourScale` because that is the scale that we used in the encoding.

Of course there are other types of legends as well. Let's for example change `"size": {"value": 200}` to `"size": {"scale": "yscale", "field": "y"}`. Our legend would then be:

```json
"legends": [
  {
    "size": "yscale"
  }
],
```

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
      {"orient": "bottom", "scale": "xscale", "grid": true},
      {"orient": "left", "scale": "yscale", "grid": true}
    ],
    "legends": [
      {
        "size": "yscale"
      }
    ],
    "marks": [
      {
        "type": "symbol",
        "from": {"data":"table"},
        "encode": {
          "enter": {
            "x": {"scale": "xscale", "field": "x"},
            "y": {"scale": "yscale", "field": "y"},
            "size": {"scale": "yscale", "field": "y"},
            "fill": {"scale": "colourScale", "field": "category"}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis1', yourVlSpec);
</script>

But wait... This doesn't look right. We'd expect that points with a larger value for `y` are larger, and that to be true for the legend as well. It seems that the yscale is the wrong way around. Also, we've lost a datapoint!

A solution to this is to create a second scale (e.g. `yscalereversed`) and use that one for the `size` and the legend. We'll still use the original `yscale` for the position along the Y-axis.

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
      "name": "yscalereversed",
      "domain": {"data": "table", "field": "y"},
      "range": "height",
      "reverse": true
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
  "legends": [
    {
      "size": "yscalereversed"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "from": {"data":"table"},
      "encode": {
        "enter": {
          "x": {"scale": "xscale", "field": "x"},
          "y": {"scale": "yscale", "field": "y"},
          "size": {"scale": "yscalereversed", "field": "y"},
          "fill": {"scale": "colourScale", "field": "category"}
        }
      }
    }
  ]
}
```

This looks more like what we expect:

<div id="vis2"></div>
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
        "name": "yscalereversed",
        "domain": {"data": "table", "field": "y"},
        "range": "height",
        "reverse": true
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
    "legends": [
      {
        "size": "yscalereversed"
      }
    ],
    "marks": [
      {
        "type": "symbol",
        "from": {"data":"table"},
        "encode": {
          "enter": {
            "x": {"scale": "xscale", "field": "x"},
            "y": {"scale": "yscale", "field": "y"},
            "size": {"scale": "yscalereversed", "field": "y"},
            "fill": {"scale": "colourScale", "field": "category"}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis2', yourVlSpec);
</script>

Why did we loose that datapoint? That's because the scale went from 0 to the height. The datapoint `{"x": 15, "y": 8, "category": "A"}` has a value of 8 (which is the smallest value), so it's mapped to one extreme of the scale. The datapoint `{"x": 35, "y": 44, "category": "C"}` (which is the largest value) is mapped to the other extreme.

{% include custom/series_vega_next.html %}
