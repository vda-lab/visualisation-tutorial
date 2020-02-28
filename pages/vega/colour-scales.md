---
title: Colour-scales
keywords: vega
sidebar: vega_sidebar
permalink: vega-colour-scales.html
folder: vega
series: vega-series
weight: 5
---
## Categorical colours
In the last exercise, we defined the colour of each bar in the data itself. It'd be better if we can let vega pick the colour for us instead. This is where _colour scales_ come into play.

Vega helps you in assigning colours to datapoints, using a collection of colouring schemes available at [https://vega.github.io/vega/docs/schemes/](https://vega.github.io/vega/docs/schemes/). Instead of hard-coding the colour for each datapoint, let's give each datapoint a category  and create a scale to assign colours.

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
      "name": "colourScale",
      "type": "ordinal",
      "domain": {"data": "table", "field": "category"},
      "range": {"scheme": "category10"}
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
          "size": {"value": 200},
          "fill": {"scale": "colourScale", "field": "category"}
        }
      }
    }
  ]
}
```

What we did here:
- We added a "category" to each datapoint. This does not have to be named "category", but can have any name.
- We created a new scale, called "colourScale". The `name`, `type` and `domain` are as we described above, but for the `range` we set `{"scheme": "category10"}`. `category10` is only one of the possible colour schemes, which are all listed on [https://vega.github.io/vega/docs/schemes/](https://vega.github.io/vega/docs/schemes/).
- For `fill` we now use the scale as well.
- Just to make the colour a bit more clear, we increased the size of the points...

The resulting plot:

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

As you can see, the points with the same category get the same colour.

## Sequential colours
What if we'd want to have the colour depend not on a nominal value such as category, but on a numerical value? Let's say, on `x`.

Change the `colourScale` to:

```json
{
  "name": "colourScale",
  "type": "linear",
  "domain": {"data": "table", "field": "x"},
  "range": {"scheme": "blues"}
}
```

and change the `field` in `encoding` -> `fill` from `category` to `x`.

You'll get this image:

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
        "name": "colourScale",
        "type": "linear",
        "domain": {"data": "table", "field": "x"},
        "range": {"scheme": "blues"}
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
            "size": {"value": 200},
            "fill": {"scale": "colourScale", "field": "x"}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis2', yourVlSpec);
</script>

{:.exercise}
**Exercise** - We use `x` both in the definition of `colourScale` and as the `field` in the `encoding`. What would it mean if we'd use `x` in the definition of `colourScale`, but `y` in the `encoding`?

{:.exercise}
**Exercise** - Try out some of the diverging colour schemes mentioned on [https://vega.github.io/vega/docs/schemes/](https://vega.github.io/vega/docs/schemes/).

If you really want to, you can also set the colours by hand. For example, we want to have categories A and B be blue, and category C be red. To do this, we simply provide an array both for `domain` and `range`, like so:

```json
{
  "name": "colourScale",
  "type": "ordinal",
  "domain": ["A","B","C"],
  "range": ["blue","blue","red"]
}
```

{% include custom/series_vega_next.html %}
