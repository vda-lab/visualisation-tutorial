---
title: Force-directed-networks
keywords: vega
sidebar: vega_sidebar
permalink: vega-force-directed-networks.html
folder: vega
series: vega-series
weight: 20
---
Let's start with a node-link diagram for a network. We'll use the miserables dataset for this.

### Minimal network
Here's a minimal vega specification, without colours or dragging:

{% highlight json %}
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "width": 350,
  "height": 250,
  "padding": 0,
  "autosize": "none",

  "signals": [
    { "name": "cx", "update": "width / 2" },
    { "name": "cy", "update": "height / 2" }
  ],

  "data": [
    {
      "name": "node-data",
      "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/miserables.json",
      "format": {"type": "json", "property": "nodes"}
    },
    {
      "name": "link-data",
      "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/miserables.json",
      "format": {"type": "json", "property": "links"}
    }
  ],

  "marks": [
    {
      "name": "nodes",
      "type": "symbol",
      "zindex": 1,

      "from": {"data": "node-data"},

      "encode": {
        "enter": {
          "fill": {"value": "grey"}
        }
      },

      "transform": [
        {
          "type": "force",
          "iterations": 300,
          "velocityDecay": 0.4,
          "forces": [
            {"force": "center", "x": {"signal": "cx"}, "y": {"signal": "cy"}},
            {"force": "collide", "radius": 5},
            {"force": "nbody", "strength": -10},
            {"force": "link", "links": "link-data", "distance": 15}
          ]
        }
      ]
    },
    {
      "type": "path",
      "from": {"data": "link-data"},
      "interactive": false,
      "encode": {
        "update": {
          "stroke": {"value": "lightgrey"},
          "strokeWidth": {"value": 0.5}
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
}
{% endhighlight %}

This is what the plot looks like:

<div id="vis1"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega/v5.json",
    "width": 350,
    "height": 250,
    "padding": 0,
    "autosize": "none",

    "signals": [
      { "name": "cx", "update": "width / 2" },
      { "name": "cy", "update": "height / 2" }
    ],

    "data": [
      {
        "name": "node-data",
        "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/miserables.json",
        "format": {"type": "json", "property": "nodes"}
      },
      {
        "name": "link-data",
        "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/miserables.json",
        "format": {"type": "json", "property": "links"}
      }
    ],

    "marks": [
      {
        "name": "nodes",
        "type": "symbol",
        "zindex": 1,

        "from": {"data": "node-data"},

        "encode": {
          "enter": {
            "fill": {"value": "grey"}
          }
        },

        "transform": [
          {
            "type": "force",
            "iterations": 300,
            "velocityDecay": 0.4,
            "forces": [
              {"force": "center", "x": {"signal": "cx"}, "y": {"signal": "cy"}},
              {"force": "collide", "radius": 5},
              {"force": "nbody", "strength": -10},
              {"force": "link", "links": "link-data", "distance": 15}
            ]
          }
        ]
      },
      {
        "type": "path",
        "from": {"data": "link-data"},
        "interactive": false,
        "encode": {
          "update": {
            "stroke": {"value": "lightgrey"},
            "strokeWidth": {"value": 0.5}
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
  };
  vegaEmbed('#vis1', yourVlSpec);
</script>

<!-- <img src="{{ site.baseurl }}/assets/vega-force-1.png" width="50%" /> -->

Let's break this down:

* `data`: If you follow the URL to the JSON file, you'll see that it looks like this: `{nodes: [], links: []}`. We create two different datasets: one for the nodes and one for the links. The `format.property` bit specifies which part needs to be extracted. It would seem that we'd be able to do this using a single dataset and creating two derived ones using `source`, but unfortunately it's not possible to extract a single element using a transform.
* `marks`: There are two types of marks, namely for the nodes and for the edges. In principle, you can draw the nodes without the edges (try it), but not the other way around because the edge positions depend on the source and target nodes.
  * For the _nodes_, everything is the same as we saw in all our previous exercises, except for the `zindex` and `transform`. The `"zindex": 1` makes sure that the nodes are drawn _on top of_ the edges.
    * `transform`: Definitely have a good look at the [documentation](https://vega.github.io/vega/docs/transforms/force/) for this. We use a single transform of type `force`. Actually, it's not just one force, but several which we list under `"forces": []`. The algorithm will try to find an equilibrium between all of these interacting forces.
      * `center`: Indicates what the center of the plot should be. This would typically be the center of your screen, i.e. `width/2` and `height/2`.
      * `collide`: To what extent should nodes be pushed apart, but only when they overlap.
      * `nbody`: To what extent should nodes be pushed apart or attracted. A negative value will push them apart; a positive one will pull them together. This value will have the largest impact on what your plot looks like.
      * `link`: While `nbody` will push nodes apart or attract them, this is contrained by the links between them.
  * For the _links_, we use `path` marks instead of `line` because the first can have arbitrary position, while lines are used for longitudinal data.
    * We set `stroke` and `strokeWidth` in an `update` section instead of `enter`. If we'd use enter, the paths wouldn't update when the nodes move around. You'd get a picture like this instead:<br/><img src="{{site.baseurl}}/assets/vega-force-link-enter.png" width="25%"/>
    * `transform`: We use the special `linkpath` transform, which is specifically for drawing a path between a source and a target. Apart from `line`, the `shape` can also be a `curve`, `arc`, `diagonal` or `orthogonal`. Try these out as well.

Here are some examples of plots with different settings for `collide`, `nbody` and `link` in the node transform:

Altering `collide`, with `nbody` equal to `-10` and `link` equal to `15`:

| `1` | `5` | `10` |
|--|--|--|
| <img src="{{ site.baseurl }}/assets/vega-force-1-10-15.png" width="25%" /> | <img src="{{ site.baseurl }}/assets/vega-force-5-10-15.png" width="25%" /> | <img src="{{ site.baseurl }}/assets/vega-force-10-10-15.png" width="25%" /> |

Altering `nbody`, with `collide` equal to `5` and `link` equal to `15`:

| `-2` | `-10` | `-20` |
|--|--|--|
| <img src="{{ site.baseurl }}/assets/vega-force-5-2-15.png" width="25%" /> | <img src="{{ site.baseurl }}/assets/vega-force-5-10-15.png" width="25%" /> | <img src="{{ site.baseurl }}/assets/vega-force-5-20-15.png" width="25%" /> |

Altering `link`, with `collide` equal to `5` and `nbody` equal to `-10`:

| `5` | `15` | `30` |
|--|--|--|
| <img src="{{ site.baseurl }}/assets/vega-force-5-10-5.png" width="25%" /> | <img src="{{ site.baseurl }}/assets/vega-force-5-10-15.png" width="25%" /> | <img src="{{ site.baseurl }}/assets/vega-force-5-10-30.png" width="25%" /> |

{:.exercise}
**Exercise** - What happens if you change the value of `nbody` to 1? Or to 10? Does the value of `collide` have an effect? If so: what effect?

### Adding node dragging
Here's an example where we can drag nodes around. It looks complex, but all should become clear when we break this example down.

{% highlight json %}
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "width": 400,
  "height": 275,
  "padding": 0,
  "autosize": "none",

  "signals": [
    { "name": "cx", "update": "width / 2" },
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

  "data": [
    {
      "name": "node-data",
      "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/miserables.json",
      "format": {"type": "json", "property": "nodes"}
    },
    {
      "name": "link-data",
      "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/miserables.json",
      "format": {"type": "json", "property": "links"}
    }
  ],

  "marks": [
    {
      "name": "nodes",
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
          "fill": {"value": "grey"}
        },
        "update": {
          "size": {"value": 50},
          "cursor": {"value": "pointer"}
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
            {"force": "collide", "radius": 5},
            {"force": "nbody", "strength": -10},
            {"force": "link", "links": "link-data", "distance": 15}
          ]
        }
      ]
    },
    {
      "type": "path",
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
}
{% endhighlight %}

Here is the result (drag one of the nodes):

<div id="vis6"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega/v5.json",
    "width": 400,
    "height": 275,
    "padding": 0,
    "autosize": "none",

    "signals": [
      { "name": "cx", "update": "width / 2" },
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

    "data": [
      {
        "name": "node-data",
        "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/miserables.json",
        "format": {"type": "json", "property": "nodes"}
      },
      {
        "name": "link-data",
        "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/miserables.json",
        "format": {"type": "json", "property": "links"}
      }
    ],

    "marks": [
      {
        "name": "nodes",
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
            "fill": {"value": "grey"}
          },
          "update": {
            "size": {"value": 50},
            "cursor": {"value": "pointer"}
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
              {"force": "collide", "radius": 5},
              {"force": "nbody", "strength": -10},
              {"force": "link", "links": "link-data", "distance": 15}
            ]
          }
        ]
      },
      {
        "type": "path",
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
  };
  vegaEmbed('#vis6', yourVlSpec);
</script>

What has changed?

* A signal `dragged` captures if anything is dragged. Possible values are: `0` (nothing is being dragged), `1` (on mouseover: something _could_ be dragged) and `2` (something is actually being dragged).
* A signal `dragged_node`, which is a container for the actual node being dragged. If the value of `dragged` is `1` (i.e. ready to drag, but not actually dragging yet), the value for `dragged_node` will be set to `item()`, which is the element on which an event is active (see [here](https://vega.github.io/vega/docs/expressions/#item)). Why do we actually check for the value of `dragged`? If you don't and start dragging a node across another one, it might happen that your mouse picks up the other node than the original one on the way.
* A signal `restart` to ensure that positions of the nodes are recalculated when we drag a node to a new position. Now how does the code `{"events": {"signal": "dragged"}, "update": "dragged > 1"}` actually work? The signal will fire every time the `dragged` signal changes. Its `update` is `dragged > 1`. `dragged > 1` is a _test_: it returns `true` or `false`. It is this `true` or `false` that will be stored in the symbol `restart`.
* A _trigger_ `dragged` on the nodes changes the `dragged_node`'s `fx` and `fy`. `fx` and `fy` are two special fields on a node object, and stand for _fixed_ x and _fixed_ y. If `dragged === 1` (i.e. the mouse hovers over the node), `fx` is set to the `x`-position of `dragged_node` and `fy` accordingly. This is so that the node stays in a fixed position while you're on top of it and does not escape from under the mouse. If `dragged` is not `1` (i.e. it's `2`), `fx` and `fy` are set to `x()` and `y()` which are the x- and y-position of the mouse. So as your mouse moves around, the node will follow.
* A trigger `!dragged`, which stands for _not dragged_. When the signal `dragged` is set to 0, `fx` and `fy` are set to `null`, meaning that the node can participate again in all forces in the network.

{:.exercise}
**Exercise** - The individuals in the miserables data belong to different groups. Use these groups to set the colour of the nodes.

{:.exercise}
**Exercise** - Create two plots next to each other: one with this network, and one with a histogram of the number of individuals per group. So something like this:<br/><img src="{{site.baseurl}}/assets/vega-force-histogram.png" width="50%" /><br/>Extra points if you can give the bars the same colour as the nodes in the graph.

<!--
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "padding": 0,
  "autosize": "none",
  "width": 800,
  "height": 400,

  "signals": [
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

  "data": [
    {
      "name": "node-data",
      "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/miserables.json",
      "format": {"type": "json", "property": "nodes"}
    },
    {
      "name": "link-data",
      "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/miserables.json",
      "format": {"type": "json", "property": "links"}
    },
    { "name": "hist-data",
      "source": "node-data",
      "transform": [
        {"type": "aggregate", "groupby": ["group"], "as": ["count"]}
      ]
    }
  ],

  "scales": [
    {
      "name": "color",
      "type": "ordinal",
      "range": {"scheme": "category10"}
    },
    { "name": "xscale",
      "type": "linear",
      "domain": [0,10],
      "range": [100,300]
    },
    { "name": "yscale",
      "type": "linear",
      "domain": [0,15],
      "range": [100,200]
    }
  ],

  "layout": {"padding": 20},

  "marks": [
    {"name": "network",
      "type": "group",
      "marks": [
        {
          "name": "nodes",
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
              "fill": {"scale": "color", "field": "group"},
              "tooltip": {"field": "name"}
            },
            "update": {
              "size": {"value": 50},
              "cursor": {"value": "pointer"}
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
                {"force": "center", "x": 200, "y": 200},
                {"force": "collide", "radius": 5},
                {"force": "nbody", "strength": -10},
                {"force": "link", "links": "link-data", "distance": 15}
              ]
            }
          ]
        },
        {
          "type": "path",
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
    {"name": "histogram",
      "type": "group",
      "marks": [
        {
          "type": "rect",
          "from": {"data":"hist-data"},
          "encode": {
            "enter": {
              "x": {"scale": "xscale", "field": "group"},
              "y2": {"value": 300},
              "width": {"value": 15},
              "height": {"scale": "yscale", "field": "count"},
              "fill": {"value": "steelblue"}
            }
          }
        }
      ]
    }
  ]
}
-->

{% include custom/series_vega_next.html %}
