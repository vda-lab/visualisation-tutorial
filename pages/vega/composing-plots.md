---
title: Composing plots
keywords: vega
sidebar: vega_sidebar
permalink: vega-composing-plots.html
folder: vega
---
Remember in vega-lite that we could create composed plots by using `concat`, `hconcat` or `vconcat`. Vega is more powerful to create layouts involving different plots. However, it is much more difficult/verbose to do so...

In the vega-lite tutorial, we created a double scatterplot for the cars data, that looked like this:

<div id="vis10"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
    "title": "Side-by-side plots",
    "data": {
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
    },
    "transform": [
      { "calculate": "year(datum.Year)", "as": "yearonly" }

    ],
    "concat": [
      {
        "mark": "circle",
        "encoding": {
          "x": {"field": "Acceleration", "type": "quantitative"},
          "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
          "color": {"field": "yearonly", "type": "ordinal"}
        }
      },
      {
        "mark": "circle",
        "encoding": {
          "x": {"field": "Horsepower", "type": "quantitative"},
          "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
          "color": {"field": "yearonly", "type": "ordinal"}
        }
      }
    ]
  };
  vegaEmbed('#vis10', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vegalite-sidebyside.png" width="50%" />
-->

If we want to recreate this using vega, here is the minimal specification:

```json
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "padding": 5,
  "data": [
    {
      "name": "cars",
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json",
      "format": {"type": "json"}
    }
  ],
  "scales": [
    {
      "name": "acceleration_xscale",
      "type": "linear",
      "domain": {"data": "cars", "field": "Acceleration"},
      "range": [0, 200],
      "nice": true,
      "zero": true
    },
    {
      "name": "mpg_yscale",
      "type": "linear",
      "domain": {"data": "cars", "field": "Miles_per_Gallon"},
      "range": [200, 0],
      "nice": true,
      "zero": true
    },
    {
      "name": "horsepower_xscale",
      "type": "linear",
      "domain": {"data": "cars", "field": "Horsepower"},
      "range": [0, 200],
      "nice": true,
      "zero": true
    }
  ],
  "layout": {"padding": 20},
  "marks": [
    {
      "type": "group",
      "encode": {
        "update": {
          "width": {"value": 200},
          "height": {"value": 200}
        }
      },
      "marks": [
        {
          "type": "symbol",
          "style": "circle",
          "from": {"data": "cars"},
          "encode": {
            "update": {
              "x": {"scale": "acceleration_xscale", "field": "Acceleration"},
              "y": {"scale": "mpg_yscale", "field": "Miles_per_Gallon"},
              "fill": {"value": "steelblue"},
              "fillOpacity": {"value": 0.5}
            }
          }
        }
      ],
      "axes": [
        {
          "scale": "mpg_yscale",
          "orient": "left",
          "gridScale": "mpg_yscale",
          "grid": true,
          "tickCount": 5,
          "title": "Miles_per_Gallon"
        },
        {
          "scale": "acceleration_xscale",
          "orient": "bottom",
          "gridScale": "acceleration_xscale",
          "grid": true,
          "tickCount": 5,
          "title": "Acceleration"
        }
      ]
    },
    {
      "type": "group",
      "style": "cell",
      "encode": {
        "update": {
          "width":  {"value": 200},
          "height": {"value": 200}
        }
      },
      "marks": [
        {
          "type": "symbol",
          "style": "circle",
          "from": {"data": "cars"},
          "encode": {
            "enter": {
              "x": {"scale": "horsepower_xscale", "field": "Horsepower"},
              "y": {"scale": "mpg_yscale", "field": "Miles_per_Gallon"},
              "fill": {"value": "steelblue"},
              "fillOpacity": {"value": 0.5}
            }
          }
        }
      ],
      "axes": [
        {
          "scale": "mpg_yscale",
          "orient": "left",
          "gridScale": "mpg_yscale",
          "grid": true,
          "tickCount": 5,
          "title": "Miles_per_Gallon"
        },
        {
          "scale": "horsepower_xscale",
          "orient": "bottom",
          "gridScale": "horsepower_xscale",
          "grid": true,
          "tickCount": 5,
          "title": "Horse power"
        }
      ]
    }
  ]
}
```

For simplicity's sake, we left out the `colourScale` and legend. Still, the specification is huge: 125 lines versus what would have taken 23 lines in vega-lite.

<div id="vis11"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega/v5.json",
    "padding": 5,
    "data": [
      {
        "name": "cars",
        "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json",
        "format": {"type": "json"}
      }
    ],
    "scales": [
      {
        "name": "acceleration_xscale",
        "type": "linear",
        "domain": {"data": "cars", "field": "Acceleration"},
        "range": [0, 200],
        "nice": true,
        "zero": true
      },
      {
        "name": "mpg_yscale",
        "type": "linear",
        "domain": {"data": "cars", "field": "Miles_per_Gallon"},
        "range": [200, 0],
        "nice": true,
        "zero": true
      },
      {
        "name": "horsepower_xscale",
        "type": "linear",
        "domain": {"data": "cars", "field": "Horsepower"},
        "range": [0, 200],
        "nice": true,
        "zero": true
      }
    ],
    "layout": {"padding": 20},
    "marks": [
      {
        "type": "group",
        "encode": {
          "update": {
            "width": {"value": 200},
            "height": {"value": 200}
          }
        },
        "marks": [
          {
            "type": "symbol",
            "style": "circle",
            "from": {"data": "cars"},
            "encode": {
              "update": {
                "x": {"scale": "acceleration_xscale", "field": "Acceleration"},
                "y": {"scale": "mpg_yscale", "field": "Miles_per_Gallon"},
                "fill": {"value": "steelblue"},
                "fillOpacity": {"value": 0.5}
              }
            }
          }
        ],
        "axes": [
          {
            "scale": "mpg_yscale",
            "orient": "left",
            "gridScale": "mpg_yscale",
            "grid": true,
            "tickCount": 5,
            "title": "Miles_per_Gallon"
          },
          {
            "scale": "acceleration_xscale",
            "orient": "bottom",
            "gridScale": "acceleration_xscale",
            "grid": true,
            "tickCount": 5,
            "title": "Acceleration"
          }
        ]
      },
      {
        "type": "group",
        "style": "cell",
        "encode": {
          "update": {
            "width":  {"value": 200},
            "height": {"value": 200}
          }
        },
        "marks": [
          {
            "type": "symbol",
            "style": "circle",
            "from": {"data": "cars"},
            "encode": {
              "enter": {
                "x": {"scale": "horsepower_xscale", "field": "Horsepower"},
                "y": {"scale": "mpg_yscale", "field": "Miles_per_Gallon"},
                "fill": {"value": "steelblue"},
                "fillOpacity": {"value": 0.5}
              }
            }
          }
        ],
        "axes": [
          {
            "scale": "mpg_yscale",
            "orient": "left",
            "gridScale": "mpg_yscale",
            "grid": true,
            "tickCount": 5,
            "title": "Miles_per_Gallon"
          },
          {
            "scale": "horsepower_xscale",
            "orient": "bottom",
            "gridScale": "horsepower_xscale",
            "grid": true,
            "tickCount": 5,
            "title": "Horse power"
          }
        ]
      }
    ]
  };
  vegaEmbed('#vis11', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vega-sidebyside.png" width="50%" />
-->

In vega, we need to set the `layout`, and the `marks` is itself an array of subplots (each containing another `marks`...).
