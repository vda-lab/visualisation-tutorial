---
title: Brushing and linking
keywords: vegalite
sidebar: vegalite_sidebar
permalink: brushing-and-linking.html
folder: vega-lite
---
Knowing how to make selections and how to make side-by-side views, we have all ingredients to create some linked-brushing plots.

### Equivalent plots
Let's first look at combinations of plots where the marks refer to the same objects: one mark in the first plot corresponds to one marks in the other plot. Below is an example script for one-way brushing: we create 2 plots, and selecting a range in the left plot will highlight plots in the right plot.

Notice that:
- We use `concat` to show two plots instead of one.
- We define `selection` in the first plot.
- We use that selection in both plots.

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "title": "Brushing and linking",
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  "concat": [
    {
      "selection": {
        "my_selection": {"type": "interval", "empty": "none"}
      },
      "mark": "circle",
      "encoding": {
        "x": {"field": "Weight_in_lbs", "type": "quantitative"},
        "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
        "color": {
          "condition": {
            "selection": "my_selection",
            "value": "red"
          },
          "value": "lightgrey"
        }
      }
    },
    {
      "mark": "circle",
      "encoding": {
        "x": {"field": "Acceleration", "type": "quantitative"},
        "y": {"field": "Horsepower", "type": "quantitative"},
        "color": {
          "condition": {
            "selection": "my_selection",
            "value": "red"
          },
          "value": "lightgrey"
        }
      }
    }
  ]
}
```

The result:

<div id="vis5"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
    "title": "Brushing and linking",
    "data": {
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
    },
    "concat": [
      {
        "selection": {
          "my_selection": {"type": "interval", "empty": "none"}
        },
        "mark": "circle",
        "encoding": {
          "x": {"field": "Weight_in_lbs", "type": "quantitative"},
          "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
          "color": {
            "condition": {
              "selection": "my_selection",
              "value": "red"
            },
            "value": "lightgrey"
          }
        }
      },
      {
        "mark": "circle",
        "encoding": {
          "x": {"field": "Acceleration", "type": "quantitative"},
          "y": {"field": "Horsepower", "type": "quantitative"},
          "color": {
            "condition": {
              "selection": "my_selection",
              "value": "red"
            },
            "value": "lightgrey"
          }
        }
      }
    ]
  };
  vegaEmbed('#vis5', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vegalite-brushinglinking.png" width="50%" />
-->

{:.exercise}
**Exercise** - Play with the code above to check what happens if (1) you define the same selection in both plots, (2) you define it only in the first plot, but only use it in the second one, (3) you define a _different_ selection in each plot and let it set the color in the second plot (i.e. selection A in plot A influences the color in plot B, and selection B in plot B sets the color in plot A.)

<!--
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "title": "Brushing and linking",
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  "concat": [
    {
      "selection": {
        "my_selection": {"type": "interval", "empty": "none"}
      },
      "mark": "circle",
      "encoding": {
        "x": {"field": "Weight_in_lbs", "type": "quantitative"},
        "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
        "color": {
          "condition": {
            "selection": "my_selection2",
            "value": "red"
          },
          "value": "lightgrey"
        }
      }
    },
    {
      "selection": {
        "my_selection2": {"type": "interval", "empty": "none"}
      },
      "mark": "circle",
      "encoding": {
        "x": {"field": "Acceleration", "type": "quantitative"},
        "y": {"field": "Horsepower", "type": "quantitative"},
        "color": {
          "condition": {
            "selection": "my_selection",
            "value": "red"
          },
          "value": "lightgrey"
        }
      }
    }
  ]
}
-->

### Non-equivalent plots
As we saw earlier, we can create histograms using transforms. Let's create a scatterplot and a histogram next to each other. We also want it to be possible to select a range in the histogram, and the corresponding points are highlighted in the scatterplot. The result will be: (interactive - brush on the histogram)

<div id="vis9"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
    "title": "Brushing and linking",
    "data": {
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
    },
    "concat": [
      {
        "mark": "circle",
        "encoding": {
          "x": {"field": "Weight_in_lbs", "type": "quantitative"},
          "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
          "color": {
            "condition": {
              "selection": "my_selection",
              "value": "red"
            },
            "value": "lightgrey"
          }
        }
      },
      {
        "selection": {
          "my_selection": {"type": "interval", "empty": "none"}
        },
        "mark": "bar",
        "encoding": {
          "x": {"bin": true, "field": "Acceleration", "type": "quantitative"},
          "y": {"aggregate": "count", "type": "quantitative"},
          "color": {
            "condition": {
              "selection": "my_selection",
              "value": "red"
            },
            "value": "lightgrey"
          }
        }
      }
    ]
  };
  vegaEmbed('#vis9', yourVlSpec);
</script>

We only have to replace the `circle` marks of the second plot as we had before, with the histogram code:

```json
...
{
  "selection": {
    "my_selection": {"type": "interval", "empty": "none"}
  },
  "mark": "bar",
  "encoding": {
    "x": {"bin": true, "field": "Acceleration", "type": "quantitative"},
    "y": {"aggregate": "count", "type": "quantitative"},
    "color": {
      "condition": {
        "selection": "my_selection",
        "value": "red"
      },
      "value": "lightgrey"
    }
  }
}
...
```
