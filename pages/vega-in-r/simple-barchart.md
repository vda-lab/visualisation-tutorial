---
title: A simple barchart
keywords: vega-in-r
sidebar: vega-in-r_sidebar
permalink: /vega-in-r-simple-barchart.html
folder: vega-in-r
series: vega-in-r-series
weight: 2
---
Here is a very simple barchart defined in altair R.

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

The dataset used for this chart is:

```R
Var1 = c("a","b","c","d","e") 
Var2 = c(11, 19, 22, 8, 14)
Var3 = c("type1","type1","type2","type1","type2")
dataset = data.frame(Var1, Var2, Var3)
```

and below is the code to generate it:


```R
chart_1 = alt$Chart(dataset)$
  mark_bar()$
  encode(
    x = "Var1:O",
    y = "Var2:Q"
  )$
  properties(
    height=200,
    width=400
  )
```

What is the syntax in altair R? It is similar to the altair Python with the major difference the usage of the operator `$` to access attributes, instead of `.`. We should note that there are some other differences of the Python and the R package described at the [Field Guide to Python Issues](https://vegawidget.github.io/altair/articles/field-guide-python.html) together with examples. Below, are the most common properties of the chart syntax:
- We first need to use the object `alt` to access the Altair API and create a chart using `alt$Chart`.
- The `data` to be visualised is called inside the `alt$Chart`.
- The `mark` used is specifed after `mark_`. Values as properties of the marks, for instance a hard-coded size or color, can be specified here.
- The `encode` determines the mapping between the channels and the data fields. The encoding that is dependent on the fields is specified here, not the encoding that has to do with values of the marks. Here, `x` and `y` are the position channels. The field type is specified after the field name. `O` stands for ordinal and `Q` for quantitative. Other types are `N` for nominal, `T` for temporal and `G` for goejson. The `x = "Var1:O"` is the short form of `x = alt$X("Var1", type = "ordinal")`. The two forms are equivalent but the long form is used when doing more adjustments unside encoding. We will see an example in the field transform section.
- The height and width of the plot is specified inside `properties`.

For more detailed references in Altair classes and functions, we may look to the [API reference](https://altair-viz.github.io/user_guide/API.html).

Now, to display the chart in Rstudio we may use `vegawidget(chart_1)` or `chart_1`. Alternatively, we can also save the chart using:
```R
htmlwidgets::saveWidget(vegawidget(chart_1),'chart_1.html')
```
and display it in the browser by opening the `chart_1.html` file.

To examine the chart specification in R we can install the package listviewer using `install.packages("listviewer")` and use:
```R
vegawidget::vw_examine(chart_1, mode = "code")
```
The output is below:

![screenshot_code]({{ site.baseurl }}/assets/screenshot_code.PNG)


{:.exercise}
**Exercise** - Make yourself comfortable with the basic syntax of the chart in the altair R. Use the color channel for `Var3` to make the chart below. Change the height and width of the panel.


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
  "height": 300,
  "mark": "bar",
  "width": 500
};
  vegaEmbed('#vis2', yourVlSpec);
</script>


{:.exercise}
**Exercise** - Visualise the same data, using a point as the mark, change the color for all points to black and visualise Var3 using size. Format the axes.



{% include custom/series_vega-in-r_next.html %}
