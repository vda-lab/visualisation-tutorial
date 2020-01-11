---
title: Selecting datapoints
keywords: vegalite
sidebar: vegalite_sidebar
permalink: selecting-datapoints.html
folder: vega-lite
---
In many cases you will want to do something more than just show a tooltip for a single datapoint, but for example select one or multiple datapoints and change their encoding, or use them to filter a different plot.

To create a selection, just add the `selection` key to your vega-lite specification. This takes an object as argument, with the following keys: `type`, `on`, and `empty`. Only `type` is mandatory, and can be `single`, `multi`, and `interval`.

The default behaviour for:
- `single`: click on a datapoint to select it.
- `multi`: click on a datapoint to select it. Hold down shift to select multiple datapoints.
- `interval`: drag the mouse to select a rectangular region

By default, all datapoints are selected. You can change this by setting `empty` to `none`.

We'll add a conditional encoding to make clear which points are selected and which are not. For the documentation on conditional formatting, see [https://vega.github.io/vega-lite/docs/condition.html](https://vega.github.io/vega-lite/docs/condition.html). See the code below how to make the colour conditional on a selection: lightgrey by default, but red if the datapoint is selected.

{% highlight json %}
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
{% endhighlight %}

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
