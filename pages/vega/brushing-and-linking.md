---
title: Brushing and linking
keywords: vega
sidebar: vega_sidebar
permalink: vega-brushing-and-linking.html
folder: vega
series: vega-series
weight: 20
---
Whereas brushing and linking in vega-lite is very simple to do, it is very hard in vega. Although it _is_ possible, you'll have to play with signals, data, and some non-documented functions within the vega code. Hopefully, brushing/linking will be easier in one of the next versions.

The idea with brushing linking is that you create a signal that captures if a mark is selected, and then letting the encoding of a mark in another plot be dependent on that signal.

For example, let's create a minimal example: we take 3 datapoints and create two plots with them. At first, we won't include any brushing/linking yet.

{% highlight json %}
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "padding": 0,
  "autosize": "none",
  "width": 400,
  "height": 220,

  "data": [
    {
      "name": "table",
      "values": [
        {"name": "point A", "a": 2, "b": 7, "c": 4},
        {"name": "point B", "a": 4, "b": 5, "c": 6},
        {"name": "point C", "a": 5, "b": 3, "c": 5}
      ]
    }
  ],

  "scales": [
    { "name": "xscale",
      "type": "linear",
      "domain": [0,10],
      "range": [0,200]
    },
    { "name": "yscale",
      "type": "linear",
      "domain": [0,10],
      "range": [0,200]
    }
  ],

  "layout": {"padding": 20},

  "marks": [
    { "name": "plot1",
      "type": "group",
      "axes": [
        {"orient": "bottom", "scale": "xscale"},
        {"orient": "right", "scale": "yscale"}
      ],
      "marks": [
        {
          "type": "symbol",

          "from": {"data": "table"},

          "encode": {
            "enter": {
              "x": {"field": "a", "scale": "xscale"},
              "y": {"field": "b", "scale": "yscale"},
              "tooltip": {"field": "name"},
              "size": {"value": 200}
            },
            "update": {
              "fill": {"value": "lightgrey"}
            }
          }
        }
      ]
    },
    { "name": "plot2",
      "type": "group",
      "axes": [
        {"orient": "bottom", "scale": "xscale"},
        {"orient": "right", "scale": "yscale"}
      ],
      "marks": [
        {
          "type": "symbol",
          "from": {"data": "table"},
          "encode": {
            "enter": {
              "x": {"field": "a", "scale": "xscale"},
              "y": {"field": "c", "scale": "yscale"},
              "size": {"value": 200},
              "tooltip": {"field": "name"}
            },
            "update": {
              "fill": {"value": "lightgrey"}
            }
          }
        }
      ]
    }
  ]
}
{% endhighlight %}

This creates two scatterplots, where the x-value is defined by feature `a` in both, and the y-value either by `b` (left) or `c` (right). The points in both plots are (from right to left): `point A`, `point B` and `point C`.

<img src="{{ site.baseurl }}/assets/vega-nobrushlink.png" width="50%" />

The colour of the datapoints in both plots is hard-coded as `lightgrey`. We will now make this plot interactive with brushing and linking: when hovering over point A in either of the plots, that same point A should be coloured red in both of them.

We can change this using the following steps, as inspired by the force-directed example from above:

* Create two signals: one for checking if you're hovering over a datapoint, and another to capture which datapoint that is.

{% highlight json %}
...
"signals": [
  { "description": "Any datapoint is activated",
    "name": "datapoint_is_activated", "value": false,
    "on": [
      {
        "events": "symbol:mouseover",
        "update": "true"
      },
      {
        "events": "symbol:mouseout",
        "update": "false"
      }
    ]
  },
  { "description": "Active datapoint",
    "name": "activated_datapoint", "value": null,
    "on": [
      {
        "events": "symbol:mouseover",
        "update": "item()"
      },
      {
        "events": "symbol:mouseout",
        "update": "null"
      }
    ]
  }
],
...
{% endhighlight %}

* Change the `fill` to test for these signals:

{% highlight json %}
...
"fill": [
  {"test": "datapoint_is_activated && datum === activated_datapoint.datum",
  "value": "red"},
  {"value": "lightgrey"}
]
...
{% endhighlight %}

Everything put together:

{% highlight json %}
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "padding": 0,
  "autosize": "none",
  "width": 400,
  "height": 220,

  "signals": [
    { "description": "Any datapoint is activated",
      "name": "datapoint_is_activated", "value": false,
      "on": [
        {
          "events": "symbol:mouseover",
          "update": "true"
        },
        {
          "events": "symbol:mouseout",
          "update": "false"
        }
      ]
    },
    { "description": "Active datapoint",
      "name": "activated_datapoint", "value": null,
      "on": [
        {
          "events": "symbol:mouseover",
          "update": "item()"
        },
        {
          "events": "symbol:mouseout",
          "update": "null"
        }
      ]
    }
  ],

  "data": [
    {
      "name": "table",
      "values": [
        {"name": "point A", "a": 2, "b": 7, "c": 4},
        {"name": "point B", "a": 4, "b": 5, "c": 6},
        {"name": "point C", "a": 5, "b": 3, "c": 5}
      ]
    }
  ],

  "scales": [
    { "name": "xscale",
      "type": "linear",
      "domain": [0,10],
      "range": [0,200]
    },
    { "name": "yscale",
      "type": "linear",
      "domain": [0,10],
      "range": [0,200]
    }
  ],

  "layout": {"padding": 20},

  "marks": [
    { "name": "plot1",
      "type": "group",
      "axes": [
        {"orient": "bottom", "scale": "xscale"},
        {"orient": "right", "scale": "yscale"}
      ],
      "marks": [
        {
          "type": "symbol",
          "from": {"data": "table"},
          "encode": {
            "enter": {
              "x": {"field": "a", "scale": "xscale"},
              "y": {"field": "b", "scale": "yscale"},
              "tooltip": {"field": "name"},
              "size": {"value": 200}
            },
              "update": {
              "fill": [
                {"test": "datapoint_is_activated && datum === activated_datapoint.datum",
                "value": "red"},
                {"value": "lightgrey"}
              ]

            }
          }
        }
      ]
    },
    { "name": "plot2",
      "type": "group",
      "axes": [
        {"orient": "bottom", "scale": "xscale"},
        {"orient": "right", "scale": "yscale"}
      ],
      "marks": [
        {
          "type": "symbol",

          "from": {"data": "table"},

          "encode": {
            "enter": {
              "x": {"field": "a", "scale": "xscale"},
              "y": {"field": "c", "scale": "yscale"},
              "size": {"value": 200},
              "tooltip": {"field": "name"}
            },
            "update": {
              "fill": [
                {"test": "datapoint_is_activated && datum === activated_datapoint.datum",
                "value": "red"},
                {"value": "lightgrey"}
              ]

            }
          }
        }
      ]
    }
  ]
}
{% endhighlight %}

The result (hover over the datapoints):
<div id="vis9"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega/v5.json",
    "padding": 0,
    "autosize": "none",
    "width": 400,
    "height": 220,

    "signals": [
      { "description": "Any datapoint is activated",
        "name": "datapoint_is_activated", "value": false,
        "on": [
          {
            "events": "symbol:mouseover",
            "update": "true"
          },
          {
            "events": "symbol:mouseout",
            "update": "false"
          }
        ]
      },
      { "description": "Active datapoint",
        "name": "activated_datapoint", "value": null,
        "on": [
          {
            "events": "symbol:mouseover",
            "update": "item()"
          },
          {
            "events": "symbol:mouseout",
            "update": "null"
          }
        ]
      }
    ],

    "data": [
      {
        "name": "table",
        "values": [
          {"name": "point A", "a": 2, "b": 7, "c": 4},
          {"name": "point B", "a": 4, "b": 5, "c": 6},
          {"name": "point C", "a": 5, "b": 3, "c": 5}
        ]
      }
    ],

    "scales": [
      { "name": "xscale",
        "type": "linear",
        "domain": [0,10],
        "range": [0,200]
      },
      { "name": "yscale",
        "type": "linear",
        "domain": [0,10],
        "range": [0,200]
      }
    ],

    "layout": {"padding": 20},

    "marks": [
      { "name": "plot1",
        "type": "group",
        "axes": [
          {"orient": "bottom", "scale": "xscale"},
          {"orient": "right", "scale": "yscale"}
        ],
        "marks": [
          {
            "type": "symbol",
            "from": {"data": "table"},
            "encode": {
              "enter": {
                "x": {"field": "a", "scale": "xscale"},
                "y": {"field": "b", "scale": "yscale"},
                "tooltip": {"field": "name"},
                "size": {"value": 200}
              },
                "update": {
                "fill": [
                  {"test": "datapoint_is_activated && datum === activated_datapoint.datum",
                  "value": "red"},
                  {"value": "lightgrey"}
                ]

              }
            }
          }
        ]
      },
      { "name": "plot2",
        "type": "group",
        "axes": [
          {"orient": "bottom", "scale": "xscale"},
          {"orient": "right", "scale": "yscale"}
        ],
        "marks": [
          {
            "type": "symbol",

            "from": {"data": "table"},

            "encode": {
              "enter": {
                "x": {"field": "a", "scale": "xscale"},
                "y": {"field": "c", "scale": "yscale"},
                "size": {"value": 200},
                "tooltip": {"field": "name"}
              },
              "update": {
                "fill": [
                  {"test": "datapoint_is_activated && datum === activated_datapoint.datum",
                  "value": "red"},
                  {"value": "lightgrey"}
                ]

              }
            }
          }
        ]
      }
    ]
  }
  vegaEmbed('#vis9', yourVlSpec);
</script>

Some observations:

* All events in the signals refer to `symbol:`-something. This is because the mark that we use is a `symbol`. If it were a rectangle we'd have to use `rect`.
* The signal `datapoint_is_activated` only captures whether any datapoint is activated (true/false).
* The signal `activated_datapoint` captures _which_ datapoint your mouse is on: that is contained in `item()` (see [here](https://vega.github.io/vega/docs/expressions/#item)).
* The `fill` is now an array instead of the simple `{"value": "lightgrey"}`. The first element of the array is a test with an associated value; the last element is the default value (i.e. when the test fails).
* In the test, we check that _both_ a datapoint is activated, and that the datapoint which the mark refers to (`datum`) is the same as the datum of the activated datapoint.

{:.exercise}
**Exercise** - Using the data at https://vda-lab.github.io/assets/stad_2910.json, create two linked plots: one with the network, and a scatterplot with `community` on the x-axis and `hadm_id` on the y-axis. Your result should be similar to the visualisation below, and highlight points between the two plots on hover (check by hovering over the points below).

<div id="vis10"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega/v5.json",
    "width": 800,
    "height": 400,
    "padding": 0,
    "autosize": "none",

    "signals": [
      { "description": "Any datapoint is activated",
        "name": "datapoint_is_activated", "value": false,
        "on": [
          {
            "events": "symbol:mouseover",
            "update": "true"
          },
          {
            "events": "symbol:mouseout",
            "update": "false"
          }
        ]
      },
      { "description": "Active datapoint",
        "name": "activated_datapoint", "value": null,
        "on": [
          {
            "events": "symbol:mouseover",
            "update": "item()"
          },
          {
            "events": "symbol:mouseout",
            "update": "null"
          }
        ]
      },
      { "name": "cx", "update": "600" },
      { "name": "cy", "update": "height / 2" },
      {
        "description": "State variable for active node dragged status.",
        "name": "dragged", "value": 0,
        "on": [
          {
            "events": "symbol:mouseout[!event.buttons], window:mouseup",
            "update": "0"
          },
          {
            "events": "symbol:mouseover",
            "update": "dragged || 1"
          },
          {
            "events": "[symbol:mousedown, window:mouseup] > window:mousemove!",
            "update": "2", "force": true
          }
        ]
      },
      {
        "description": "Graph node most recently interacted with.",
        "name": "dragged_node", "value": null,
        "on": [
          {
            "events": "symbol:mouseover",
            "update": "dragged === 1 ? item() : dragged_node"
          }
        ]
      },
      {
        "description": "Flag to restart Force simulation upon data changes.",
        "name": "restart", "value": false,
        "on": [
          {"events": {"signal": "dragged"}, "update": "dragged > 1"}
        ]
      }
    ],

    "scales": [
      {
        "name": "xscale",
        "type": "linear",
        "domain": {"data": "node-data", "field": "community"},
        "range": [100, 300]
      },
      {
        "name": "yscale",
        "type": "linear",
        "domain": {"data": "node-data", "field": "hadm_id"},
        "range": [200, 50]
      },
      {"name": "colourScale",
        "type": "ordinal",
        "domain": {"data": "node-data", "field": "community"},
        "range": {"scheme": "category20"}
      }
    ],

    "data": [
      {
        "name": "node-data",
        "url": "https://vda-lab.github.io/assets/stad_2910.json",
        "format": {"type": "json", "property": "nodes"}
      },
      {
        "name": "link-data",
        "url": "https://vda-lab.github.io/assets/stad_2910.json",
        "format": {"type": "json", "property": "links"}
      }
    ],
    "marks": [
      { "type": "group",
        "encode": {
          "update": {
            "width": {"value": 200},
            "height": {"value": 200}
          }
        },
        "marks": [
          { "name": "nodes",
            "type": "symbol",
            "zindex": 1,

            "from": {"data": "node-data"},
            "on": [
              {
                "trigger": "dragged",
                "modify": "dragged_node",
                "values": "dragged === 1 ? {fx:dragged_node.x, fy:dragged_node.y} : {fx:x(), fy:y()}"
              },
              {
                "trigger": "!dragged",
                "modify": "dragged_node", "values": "{fx: null, fy: null}"
              }
            ],

            "encode": {
              "enter": {
                "fill": {"value": "grey"},
                "fillOpacity": {"value": 0.8}
              },
              "update": {
                "zindex": [
                  { "test": "datapoint_is_activated && datum === activated_datapoint.datum", "value": -1 }
                ],
                "size": [
                      {"test": "datapoint_is_activated && datum === activated_datapoint.datum",
                      "value": 200},
                      {"value": 50}
                    ],
                "cursor": {"value": "pointer"},
                "fill": [
                      {"test": "datapoint_is_activated && datum === activated_datapoint.datum",
                      "value": "red"},
                      {"field": "community", "scale": "colourScale"}
                    ]
              }
            },

            "transform": [
              {
                "type": "force",
                "iterations": 300,
                "velocityDecay": 0.4,
                "restart": {"signal": "restart"},
                "static": false,
                "forces": [
                  {"force": "center", "x": {"signal": "cx"}, "y": {"signal": "cy"}},
                  {"force": "collide", "radius": 2},
                  {"force": "nbody", "strength": -1},
                  {"force": "link", "links": "link-data", "distance": 5}
                ]
              }
            ]
          },
          { "type": "path",
            "from": {"data": "link-data"},
            "interactive": false,
            "encode": {
              "update": {
                "stroke": {"value": "lightgrey"}
              }
            },
            "transform": [
              {
                "type": "linkpath", "shape": "line",
                "sourceX": "datum.source.x", "sourceY": "datum.source.y",
                "targetX": "datum.target.x", "targetY": "datum.target.y"
              }
            ]
          }
        ]
      },
      { "type": "group",
        "encode": {
          "update": {
            "width": {"value": 200},
            "height": {"value": 200}
          }
        },
        "marks": [
          { "type": "symbol",
            "from": {"data": "node-data"},
            "encode": {
              "enter": {
                "x": {"field": "community", "scale": "xscale"},
                "y": {"field": "hadm_id", "scale": "yscale"},
                "tooltip": {"field": "hadm_id"}
              },
              "update": {
                "zindex": [
                  { "test": "datapoint_is_activated && datum === activated_datapoint.datum", "value": -1 }
                ],
                "fill": [
                      {"test": "datapoint_is_activated && datum === activated_datapoint.datum",
                      "value": "red"},
                      {"field": "community", "scale": "colourScale"}
                    ],
                "size": [
                      {"test": "datapoint_is_activated && datum === activated_datapoint.datum",
                      "value": 200},
                      {"value": 50}
                    ]
              }
            }
          }
        ],
        "axes": [
          {
            "scale": "xscale",
            "orient": "bottom",
            "title": "Community"
          },
          {
            "scale": "yscale",
            "orient": "right",
            "offset": {"value": 120},
            "title": "hadm_id"
          }
        ]
      }
    ]
  }
  vegaEmbed('#vis10', yourVlSpec);
</script>

{% include custom/series_vega_next.html %}
