---
title: Event streams
keywords: vega
sidebar: vega_sidebar
permalink: vega-event-streams.html
folder: vega
series: vega-series
weight: 14
---
As per the [documentation](https://vega.github.io/vega/docs/event-streams/): "Event streams are the primary means of modelling user input to enable dynamic, interactive visualisations. Event streams capture a **sequence of input events** such as mouse click, touch movement, timer ticks, or signal updates. When events that match a stream definition occur, they **cause any corresponding signal event handlers to evaluate**, potentially updating a signal value."

Events are not described in their separate section in the vega specification, but within the signals that get triggered when an event happens. For example, the following code makes a signal `mouseX` available which is updated every time the mouse is moved. This signal is then used in the `marks` section to display that position.

```json
...
"signals": [
  {
    "name": "mouseX",
    "on": [
      {"events":"mousemove", "update": "event.x"}
    ]
  }
],
...
"marks": [
  {
    "type": "text",
    "encode": {
      "enter": {
        "x": {"value": 10},
        "y": {"value": 10}
      },
      "update": {
        "text": {"signal": "mouseX"}
      }
    }
  }
]
...
```

Move your mouse over the plot below:

<div id="vis4"></div>
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
        "name": "mouseX",
        "on": [
          {"events":"mousemove", "update": "event.x"}
        ]
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
          }
        }
      },
      {
        "type": "text",
        "encode": {
          "enter": {
            "x": {"value": 10},
            "y": {"value": 10},
            "fontSize": {"value": 42}
          },
          "update": {
            "text": {"signal": "mouseX"}
          }
        }
      }
    ]
  };
  vegaEmbed('#vis4', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vega-noscaleinversion.png" width="50%"/>
-->

Note that now we have seen 3 different ways to define the value to use for setting parameters:

* `"value"`, e.g. `"x": {"value": 10}` for fixed values
* `"field"`, e.g. `"x": {"field": "Acceleration"}` for values that are dependent on the dataset
* `"signal"`, e.g. `"x": {"signal": "mouseX"}` for values that can change over time

Notice in this code that we put the `"text"` part within `"update"` and not within `"enter"`. This is because what is defined in `"enter"` is only read once. Any parameters that do not change can be put there, though.

Event types that you can use include `click`, `cblclick`, `dragenter`, `dragleave`, `mousedown`, `mouseup`, `mousemove`, etc. For the full list, see [https://vega.github.io/vega/docs/event-streams/](https://vega.github.io/vega/docs/event-streams/).

These event types can be applied to different _sources_: the screen (e.g. a `mousemove` on the screen), any mark (e.g. `rect:click`), or a particular mark (e.g. `@mymark:dragenter`). Some more examples of event types applied to different sources (again from the documentation):

| Event                      | What it does                                       |
|:-------------------------- |:---------------------------------------------------|
| `mousedown`                | capture all mousedown events, regardless of source |
| `*:mousedown`              | mousedown events on marks, but not the view itself |
| `rect:mousedown`           | mousedown events on any rect marks                 |
| `@foo:mousedown`           |  mousedown events on marks named 'foo'             |
| `window:mousemove`         | capture mousemove events from the browser window   |
| `timer{1000}`              | capture a timer tick every 1000 ms                 |
| `mousemove[event.buttons]` | mousemove events with any mouse button pressed     |
| `click[event.shiftKey]`    | click events with the shift key pressed            |

If you know CSS, this syntax will be particularly familiar to you.

{:.exercise}
**Exercise** - Change the image above so that the number is not continuously updated, but only when you click on one of the datapoints.

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
      "name": "mouseX",
      "on": [
        {"events":"symbol:click", "update": "event.x"}
      ]
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
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {"value": 10},
          "y": {"value": 10},
          "fontSize": {"value": 42}
        },
        "update": {
          "text": {"signal": "mouseX"}
        }
      }
    }
  ]
}
-->

{:.exercise}
**Exercise** - Change the plot so that the size of the points changes based on the horizontal position of the mouse: if the mouse is on the left of the image the points should be small, if it is on the right of the image the points should be large.

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
    {"name": "mouseX", "on": [{"events": "mousemove", "update": "event.x"}]}
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
    },
    {
      "name": "sizeScale",
      "domain": [0, 1000],
      "range": [1, 400]
    }
  ],
  "axes": [
    {"orient": "bottom", "scale": "xscale", "grid": true},
    {"orient": "left", "scale": "yscale", "grid": true}
  ],
  "marks": [
    {
      "type": "symbol",
      "from": {"data": "cars"},
      "encode": {
        "enter": {
          "x": {"scale": "xscale", "field": "Acceleration"},
          "y": {"scale": "yscale", "field": "Miles_per_Gallon"},
          "fillOpacity": {"value": 0.5}
        },
        "update": {
          "size": {"signal": "mouseX", "scale": "sizeScale"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {"value": 10},
          "y": {"value": 10},
          "fontSize": {"value": 42}
        },
        "update": {"text": {"signal": "mouseX"}}
      }
    }
  ]
}
-->

{% include custom/series_vega_next.html %}
