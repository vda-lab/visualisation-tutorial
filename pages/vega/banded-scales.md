---
title: Banded scales
keywords: vega
sidebar: vega_sidebar
permalink: vega-banded-scales.html
folder: vega
series: vega-series
weight: 6
---
One of the types of scales is the `band`. From the documentation: "_Band scales (band) accept a discrete domain similar to ordinal scales, but map this domain to a continuous, numeric output range such as pixels. Discrete output values are automatically computed by the scale by dividing the continuous range into uniform bands. Band scales are typically used for bar charts with an ordinal or categorical dimension._" An example of this is a heatmap. Such heatmap can be created in two different ways: as we would have done before by creating squares, or using bands as shown below.

```json
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "width": 300,
  "height": 300,
  "padding": 5,

  "data": [
    {
      "name": "similarities",
      "url": "https://gist.githubusercontent.com/jandot/3690c4da411245cfc9eada1329d787a1/raw/04bdb13d3e65b5ad6d014f37f535833d336b90ad/tissue_similarities.csv",
      "format": {"type": "csv", "parse": {"tissue1": "string", "tissue2": "string", "similarity": "number"}}
    }
  ],

  "scales": [
    {
      "name": "xScale",
      "type": "band",
      "domain": {"data": "similarities", "field": "tissue1"},
      "range": "width"
    },
    {
      "name": "yScale",
      "type": "band",
      "domain": {"data": "similarities", "field": "tissue2"},
      "range": "height"
    },
    {
      "name": "colourScale",
      "type": "linear",
      "range": {"scheme": "blueorange"},
      "domain": [-0.5,0.5]
    }
  ],

  "marks": [
    {
      "type": "rect",
      "from": {"data": "similarities"},
      "encode": {
        "enter": {
          "x": {"field": "tissue1", "scale": "xScale"},
          "y": {"field": "tissue2", "scale": "yScale"},
          "width": {"scale": "xScale", "band": 1},
          "height": {"scale": "yScale", "band": 1},
          "tooltip": {"signal": "datum.tissue1 + ' vs ' + datum.tissue2 + ': ' + datum.similarity"}
        },
        "update": {
          "fill": {"scale": "colourScale", "field": "similarity"}
        }
      }
    }
  ]
}
```

<div id="vis1"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega/v5.json",
    "width": 300,
    "height": 300,
    "padding": 5,

    "data": [
      {
        "name": "similarities",
        "url": "https://gist.githubusercontent.com/jandot/3690c4da411245cfc9eada1329d787a1/raw/04bdb13d3e65b5ad6d014f37f535833d336b90ad/tissue_similarities.csv",
        "format": {"type": "csv", "parse": {"tissue1": "string", "tissue2": "string", "similarity": "number"}}
      }
    ],

    "scales": [
      {
        "name": "xScale",
        "type": "band",
        "domain": {"data": "similarities", "field": "tissue1"},
        "range": "width"
      },
      {
        "name": "yScale",
        "type": "band",
        "domain": {"data": "similarities", "field": "tissue2"},
        "range": "height"
      },
      {
        "name": "colourScale",
        "type": "linear",
        "range": {"scheme": "blueorange"},
        "domain": [-0.5,0.5],
        "zero": false, "nice": true
      }
    ],

    "marks": [
      {
        "type": "rect",
        "from": {"data": "similarities"},
        "encode": {
          "enter": {
            "x": {"field": "tissue1", "scale": "xScale"},
            "y": {"field": "tissue2", "scale": "yScale"},
            "width": {"scale": "xScale", "band": 1},
            "height": {"scale": "yScale", "band": 1},
            "tooltip": {"signal": "datum.tissue1 + ' vs ' + datum.tissue2 + ': ' + datum.similarity"}
          },
          "update": {
            "fill": {"scale": "colourScale", "field": "similarity"}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis1', yourVlSpec);
</script>

{:.exercise}
**Exercise** - Add the colour legend to this plot.

{% include custom/series_vega_next.html %}
