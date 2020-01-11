---
title: Using widgets to send signals
keywords: vega
sidebar: vega_sidebar
permalink: vega-using-widgets-to-send-signals.html
folder: vega
---
Sometimes it'd be nice to make a plot interactive so that you can set parameters without having to dive into the vega specification. We can use signals for this.

**Setting colour using a dropdown box**

We can create a "colourSelector" signal (the name is arbitrary), which is bound to an input widget using `"bind": {"input": "select", "options": ["black","steelblue","red"]}`. The default value can be set in the `signals` pragma itself as well. In the mark encoding, we can set `"fill": {"signal": "colourSelector"}`. But make sure to do this in an `update` section and not in `enter`, as this value will change.

```json
{
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
  "signals": [
    {
      "name": "colourSelector",
      "bind": {"input": "select", "options": ["black","steelblue","red"]},
      "value": "red"
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
          "fillOpacity": {"value": 0.5}
        },
        "update": {
          "fill": {"signal": "colourSelector"}
        }
      }
    }
  ]
}
```

<div id="vis5"></div>
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
    "signals": [
      {
        "name": "colourSelector",
        "bind": {"input": "select", "options": ["black","steelblue","red"]},
        "value": "red"
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
            "fillOpacity": {"value": 0.5}
          },
          "update": {
            "fill": {"signal": "colourSelector"}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis5', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vega-colourselector.png" width="50%" />
-->

**Selecting a value using a slider**

We can also hide the datapoints that do not comply to a given filter, e.g. on number of cylinders:

```json
{
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
  "signals": [
    {
      "name": "colourSelector",
      "bind": {"input": "select", "options": ["black","steelblue","red"]},
      "value": "red"
    },
    {
      "name": "cylinderSelector",
      "bind": {"input": "range", "min": 3, "max": 8, "step": 1},
      "value": 4
    },
    {
      "name": "test"
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
          "y": {"scale": "yscale", "field": "Miles_per_Gallon"}
        },
        "update": {
          "fillOpacity": {"signal": "datum.Cylinders == cylinderSelector ? 0.5 : 0"},
          "fill": {"signal": "colourSelector"}
        }
      }
    }
  ]
}
```

<div id="vis8"></div>
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
    "signals": [
      {
        "name": "colourSelector",
        "bind": {"input": "select", "options": ["black","steelblue","red"]},
        "value": "red"
      },
      {
        "name": "cylinderSelector",
        "bind": {"input": "range", "min": 3, "max": 8, "step": 1},
        "value": 4
      },
      {
        "name": "test"
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
            "y": {"scale": "yscale", "field": "Miles_per_Gallon"}
          },
          "update": {
            "fillOpacity": {"signal": "datum.Cylinders == cylinderSelector ? 0.5 : 0"},
            "fill": {"signal": "colourSelector"}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis8', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vega-colourcylinderselector.png" width="50%" />
-->

{:.exercise}
**Exercise** - In the Transform section above, we created a filtered dataset containing only European cars. This dataset was called `euro-cars`. We could do the same for American and Japanese cars, calling them `us-cars` and `japanese-cars`. To actually use one of these more specific datasets for the marks, we had to change `"from": {"data":"cars"}` to `"from": {"data":"euro-cars"}` in the code. Although this is good for when you're developing your visualisation, it'd be much better if we didn't have to dive into the code just to select the dataset. Create a dropdown box that let's you choose which of the three regions of origin to choose, using the `fillOpacity` trick we used above.

<!--
{
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
  "signals": [
    {
      "name": "originSelector",
      "bind": {"input": "select", "options": ["USA","Europe","Japan"]},
      "value": "Europe"
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
          "fill": {"value": "steelblue"}
        },
        "update": {
          "fillOpacity": {"signal": "datum.Origin == originSelector ? 0.5 : 0"}
        }
      }
    }
  ]
}
-->

{:.exercise}
**Exercise** - Now try to do the same thing where, instead of using this opacity trick, you actually define a filtered dataset that contains only the data for the region that you select using the dropdown box.

<!--
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "width": 400,
  "height": 200,
  "padding": 5,

  "data": [
    {
      "name": "cars",
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
    },
    {
      "name": "cars-by-origin",
      "source": "cars",
      "transform": [
        {"type": "filter", "expr": "datum.Origin == originSelector"}
      ]
    }

  ],
  "signals": [
    {
      "name": "originSelector",
      "bind": {"input": "select", "options": ["USA","Europe","Japan"]},
      "value": "Europe"
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
      "from": {"data":"cars-by-origin"},
      "encode": {
        "enter": {
          "x": {"scale": "xscale", "field": "Acceleration"},
          "y": {"scale": "yscale", "field": "Miles_per_Gallon"},
          "fill": {"value": "steelblue"},
          "fillOpacity": {"value": 0.5}
        }
      }
    }
  ]
}
-->
