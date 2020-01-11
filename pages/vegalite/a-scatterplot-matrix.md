---
title: A scatterplot matrix
keywords: vegalite
sidebar: vegalite_sidebar
permalink: a-scatterplot-matrix.html
folder: vega-lite
---
We've now seen how to do brushing and linking across different plots. One of the typical use cases is the scatterplot matrix. Based on what we've seen above, we can already create this, just by adding specifications to the `concat` section.

{:.exercise}
**Exercise** - Create a scatterplot matrix of the features `Weight_in_lbs`, `Miles_per_Gallon` and  `Acceleration` with linking and brushing as we did above.

When doing the exercise, you'll notice that there is a lot of repetition, as the `selection`, `marks` and `encoding` are repeated for each plot. For this use case, vega-lite provides the `repeat` keyword. It allows you to extract the variable part of the specification into a separate array. When you do this, you'll have to put the `selection`, `marks` and `encoding` within a separate `spec` again.

{% highlight json %}
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "title": "Scatterplot matrix",
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  "repeat": {
    "column": [ "Weight_in_lbs", "Miles_per_Gallon", "Acceleration" ],
    "row": [ "Weight_in_lbs", "Miles_per_Gallon", "Acceleration" ]
  },
  "spec": {
    "selection": {
      "my_selection": {"type": "interval", "empty": "none"}
    },
    "mark": "circle",
    "encoding": {
      "x": {"field": {"repeat": "column"}, "type": "quantitative"},
      "y": {"field": {"repeat": "row"}, "type": "quantitative"},
      "color": {
        "condition": {
          "selection": "my_selection",
          "value": "red"
        },
        "value": "lightgrey"
      }
    }
  }
}
{% endhighlight %}

This will give you this image. Try selecting a group of datapoints.

<div id="vis7"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
    "title": "Scatterplot matrix",
    "data": {
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
    },
    "repeat": {
      "column": [ "Weight_in_lbs", "Miles_per_Gallon", "Acceleration" ],
      "row": [ "Weight_in_lbs", "Miles_per_Gallon", "Acceleration" ]
    },
    "spec": {
      "selection": {
        "my_selection": {"type": "interval", "empty": "none"}
      },
      "mark": "circle",
      "encoding": {
        "x": {"field": {"repeat": "column"}, "type": "quantitative"},
        "y": {"field": {"repeat": "row"}, "type": "quantitative"},
        "color": {
          "condition": {
            "selection": "my_selection",
            "value": "red"
          },
          "value": "lightgrey"
        }
      }
    }
  };
  vegaEmbed('#vis7', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vegalite-splom.png" />
-->
