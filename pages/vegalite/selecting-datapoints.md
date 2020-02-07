---
title: Selecting datapoints
keywords: vegalite
sidebar: vegalite_sidebar
permalink: vegalite-selecting-datapoints.html
folder: vega-lite
series: vegalite-series
weight: 9
---
In many cases you will want to do something more than just show a tooltip for a single datapoint, but for example select one or multiple datapoints and change their encoding, or use them to filter a different plot.

To create a selection, add the `selection` key to your vega-lite specification. This takes an object as argument, with the following keys: `type`, `on`, and `empty`. Only `type` is mandatory, and can be `single`, `multi`, and `interval`.

```text
"selection": {
  "my_selection": {"type": "interval"}
}
```

The key `my_selection` is the name that we want to give to this selection, and which we can use further down where we actually want to use it.

The default behaviour for:
- `single`: click on a datapoint to select it.
- `multi`: click on a datapoint to select it. Hold down shift to select multiple datapoints.
- `interval`: drag the mouse to select a rectangular region

By default, all datapoints are selected. You can change this by setting `empty` to `none`.

We'll add a conditional encoding to make clear which points are selected and which are not. Instead of using a `{"field": ...}` for `color`, we now use a `condition` in addition to `value`: if the condition with a particular name is true, then the value within the condition will be used (in this case: red), else the default colour is used (in this case lightgrey).

```text
"color": {
  "condition": {
    "selection": <name_of_my_selection>,
    "value": "red"
  },
  "value": "lightgrey"
}
```

For the documentation on conditional formatting, see [https://vega.github.io/vega-lite/docs/condition.html](https://vega.github.io/vega-lite/docs/condition.html). See the code below how to make the colour conditional on a selection: lightgrey by default, but red if the datapoint is selected.

```json
{
  "title": "Making selections",
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  "selection": {
    "my_selection": {"type": "interval", "empty": "none"}
  },
  "mark": "circle",
  "encoding": {
    "x": {"field": "Acceleration", "type": "quantitative"},
    "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
    "color": {
      "condition": {
        "selection": "my_selection",
        "value": "red"
      },
      "value": "lightgrey"
    }
  }
}
```

This will give you the image below. Try dragging your mouse.

<div id="vis3"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "title": "Making selections",
    "data": {
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
    },
    "selection": {
      "my_selection": {"type": "interval", "empty": "none"}
    },
    "mark": "circle",
    "encoding": {
      "x": {"field": "Acceleration", "type": "quantitative"},
      "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
      "color": {
        "condition": {
          "selection": "my_selection",
          "value": "red"
        },
        "value": "lightgrey"
      }
    }
  };
  vegaEmbed('#vis3', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vegalite-selection.png" width="50%" />
-->

You can have multiple selections defined as well. We can for example extend the above example so that datapoints that are selected with a mouse-drag are red, while those selected with a mouse-click are green. For this, we'll create an additional selection (and in the process, we'll use a better name as well):

```text
"selection": {
  "my_selection_drag": {"type": "interval", "empty": "none"},
  "my_selection_click": {"type": "single", "empty": "none"}
}
```

Instead of `color` taking an object as above, we'll have to give it an array instead:

```text
"color": {
  "condition": [{
      "selection": "my_selection_drag",
      "value": "red"
    },
    {
      "selection": "my_selection_click",
      "value": "green"
    }
  ],
  "value": "lightgrey"
}
```

{:.exercise}
**Exercise** - Adapt the plot above with these requirements: (1) select only a single datapoint instead of an interval, (2) the datapoint should be selected by mouseover, not by click, and (3) in addition to the color changing, the size of the datapoint should be 120 instead of a default of 20.

<!--
{
  "title": "Making selections",
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  "selection": {
    "my_selection": {"type": "single", "on": "mouseover", "empty": "none"}
  },
  "mark": "circle",
  "encoding": {
    "x": {"field": "Acceleration", "type": "quantitative"},
    "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
    "color": {
      "condition": {
        "selection": "my_selection",
        "value": "red"
      },
      "value": "lightgrey"
    },
    "size": {
      "condition": {
        "selection": "my_selection",
        "value": 120
      },
      "value": 20
    }
  }
}
-->

{% include custom/series_vegalite_next.html %}
