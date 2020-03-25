---
title: Simple Interaction
keywords: vega-in-r
sidebar: vega-in-r_sidebar
permalink: /vega-in-r-simple-interaction.html
folder: vega-in-r
series: vega-in-r-series
weight: 4
---

One of the main advantages to use the altair package is the fact that supports the generation of interactive graphics. The code required for adding a simple interaction is relatively short.

## Tooltip

A tooltip can be added to the plot using `tooltip()` inside encode. For one variable displayed in the tooltip we can use:

```R
...
tooltip = "Variable_1"
...
```

and for more than one variable, we can use the R function c() as illustrated below:

```R
...
tooltip = c("Variable_1", "Variable_2")
...
```

Mind that if you are importing the data from a url directly in the plot specification, you may need to specify the field type.


<div id="vis6"></div>
<script type="text/javascript">
    var yourVlSpec = {
  "$schema": "https://vega.github.io/schema/vega-lite/v4.0.0.json",
  "config": {
    "view": {
      "continuousHeight": 300,
      "continuousWidth": 400
    }
  },
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv"
  },
  "encoding": {
    "color": {
      "field": "Entity",
      "type": "nominal"
    },
    "opacity": {
      "field": "Deaths",
      "type": "quantitative"
    },
    "tooltip": [
      {
        "field": "Year",
        "type": "ordinal"
      },
      {
        "field": "Deaths",
        "type": "quantitative"
      }
    ],
    "x": {
      "field": "Entity",
      "type": "ordinal"
    },
    "y": {
      "field": "Year",
      "type": "ordinal"
    }
  },
  "height": 600,
  "mark": "rect",
  "transform": [
    {
      "filter": {
        "field": "Entity",
        "oneOf": [
          "Drought",
          "Earthquake",
          "Epidemic",
          "Extreme temperature",
          "Extreme weather",
          "Flood",
          "Landslide",
          "Mass movement (dry)",
          "Volcanic activity",
          "Wildfire"
        ]
      }
    }
  ],
  "width": 200
};
  vegaEmbed('#vis6', yourVlSpec);
</script>

{:.exercise}
**Exercise** - Add a tooltip in the heatmap we created in the previous section, to get the graph illustrated above.


## Zooming and Panning

We illustrate two ways of making a graph zoomable and pannable. The first one is by adding the `intreactive()` attribute, as illustrated below:

```R
$interactive()
```

A second option is to specify the selection outside the plot code and then use it inside the `add_selection` attribute in the chart code.
The second option is an interval selection using a scale binding. 

```R
selection = alt$selection_interval(bind='scales')

chart = alt$Chart(data_source_subset)$
.....
$add_selection(
    selection
  )
```

<div id="vis7"></div>
<script type="text/javascript">
    var yourVlSpec = {
  "$schema": "https://vega.github.io/schema/vega-lite/v4.0.0.json",
  "config": {
    "view": {
      "continuousHeight": 300,
      "continuousWidth": 400
    }
  },
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv"
  },
  "encoding": {
    "tooltip": [
      {
        "field": "Year",
        "type": "ordinal"
      },
      {
        "field": "Deaths",
        "type": "quantitative"
      }
    ],
    "x": {
      "field": "Year",
      "type": "quantitative"
    },
    "y": {
      "field": "Deaths",
      "type": "quantitative"
    }
  },
  "height": 300,
  "mark": "line",
  "selection": {
    "selector003": {
      "bind": "scales",
      "encodings": [
        "x",
        "y"
      ],
      "type": "interval"
    }
  },
  "transform": [
    {
      "filter": {
        "equal": "All natural disasters",
        "field": "Entity"
      }
    }
  ],
  "width": 600
};
  vegaEmbed('#vis7', yourVlSpec);
</script>


{:.exercise}
**Exercise** - Make the time series plot of all natural distasters interactive, to get the graph illustrated above. Use both ways of making it zoomable and pannable.

{:.exercise}
**Exercise** - Go through the other selection types supported in altair. [https://altair-viz.github.io/user_guide/generated/api/altair.selection_interval.html#altair.selection_interval.html](https://altair-viz.github.io/user_guide/generated/api/altair.selection_interval.html#altair.selection_interval)


{% include custom/series_vega-in-r_next.html %}
