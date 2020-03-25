---
title: A simple barchart
keywords: vega-in-r
sidebar: vega-in-r_sidebar
permalink: /vega-in-r-simple-barchart.html
folder: vega-in-r
series: vega-in-r-series
weight: 2
---
Here is a very simple barchart defined in altair in R.

<div id="vis1"></div>
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
    "name": "data-c15a74353a288269433adfdc7c0ad142"
  },
  "datasets": {
    "data-c15a74353a288269433adfdc7c0ad142": [
      {
        "Var1": "a",
        "Var2": 11,
        "Var3": "type1"
      },
      {
        "Var1": "b",
        "Var2": 19,
        "Var3": "type1"
      },
      {
        "Var1": "c",
        "Var2": 22,
        "Var3": "type2"
      },
      {
        "Var1": "d",
        "Var2": 8,
        "Var3": "type1"
      },
      {
        "Var1": "e",
        "Var2": 14,
        "Var3": "type2"
      }
    ]
  },
  "encoding": {
    "x": {
      "field": "Var1",
      "type": "ordinal"
    },
    "y": {
      "field": "Var2",
      "type": "quantitative"
    }
  },
  "height": 200,
  "mark": "bar",
  "width": 400
};
  vegaEmbed('#vis1', yourVlSpec);
</script>

The dataset of the chart is:

```R
Var1 = c("a","b","c","d","e") 
Var2 = c(11, 19, 22, 8, 14)
Var3 = c("type1","type1","type2","type1","type2")
dataset = data.frame(Var1, Var2, Var3)
```

and below is the code used to generate it:


```R
chart_1 = 
  alt$Chart(dataset)$
  mark_bar()$
  encode(
    x = "Var1:O",
    y = "Var2:Q"
    # color = "Var3:N"
  )$properties(
    height=200,
    width=400
  )
```

What is the syntax in the altair R? It is similar to the Python altair and the major difference is the usage of the operator `$` to access attributes, instead of `.`.
We use the object `alt` to access the Altair API and the first basic argument is the `alt$Chart`.
- The `data` to be visualised is called inside the `alt$Chart`.
- The `mark` is specifed after `mark_`.
- The `encoding` determines the mapping between the channels and the data. Here, `x` and `y` are the position channels. The field type is specified after the field name. `O` stands for ordinal and `Q` for quantitative.
- The height and width of the plot is specified inside `properties`.


{:.exercise}
**Exercise** - Make yourself comfortable with the syntax of this basic altair chart. Use the color channel for `Var3` to make the chart below. Then, change the mark and add a variable for size.

<div id="vis2"></div>
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
    "name": "data-c15a74353a288269433adfdc7c0ad142"
  },
  "datasets": {
    "data-c15a74353a288269433adfdc7c0ad142": [
      {
        "Var1": "a",
        "Var2": 11,
        "Var3": "type1"
      },
      {
        "Var1": "b",
        "Var2": 19,
        "Var3": "type1"
      },
      {
        "Var1": "c",
        "Var2": 22,
        "Var3": "type2"
      },
      {
        "Var1": "d",
        "Var2": 8,
        "Var3": "type1"
      },
      {
        "Var1": "e",
        "Var2": 14,
        "Var3": "type2"
      }
    ]
  },
  "encoding": {
    "color": {
      "field": "Var3",
      "type": "nominal"
    },
    "x": {
      "field": "Var1",
      "type": "ordinal"
    },
    "y": {
      "field": "Var2",
      "type": "quantitative"
    }
  },
  "height": 200,
  "mark": "bar",
  "width": 400
};
  vegaEmbed('#vis2', yourVlSpec);
</script>

{:.exercise}
**Exercise** - Change the height and width of the panel and remake the plot above.


{% include custom/series_vega-in-r_next.html %}
