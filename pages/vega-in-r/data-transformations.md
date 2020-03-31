---
title: Data Transform
keywords: vega-in-r
sidebar: vega-in-r_sidebar
permalink: /vega-in-r-data-transformations.html
folder: vega-in-r
series: vega-in-r-series
weight: 6
---

As mentioned in the documentation of altair, [https://altair-viz.github.io/user_guide/transform/index.html](https://altair-viz.github.io/user_guide/transform/index.html) in most cases, it is suggested to perform transformations outside the chart definition, so in our case using R. Of course, data transforms inside the chart can also be useful in some cases.
So far, we have been filtering the data in R and then using the modified data in the chart specification. Now, we use the `transform_filter()` to subset the data inside the chart. We make the linechart we have seen in a previous section using the code below:

```R
chart_disasters = alt$Chart("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv")$
  mark_line()$
  encode(
    x = 'Year:Q',
    y = 'Deaths:Q',
    tooltip = c("Year", "Deaths")
  )$
  properties(
    height = 300,
    width = 600
  )$
  transform_filter(
   alt$FieldEqualPredicate(field = "Entity", equal = "All natural disasters")
  )
```

<div id="vis13"></div>
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
  vegaEmbed('#vis13', yourVlSpec);
</script>

<br/>

We use the field predicates to assess whether a data point satisfied certain conditions. As mentioned in the [field predicates reference](https://altair-viz.github.io/user_guide/transform/filter.html#field-predicates) the `FieldEqualPredicate` evaluates whether a field is equal to a particular value. The variable is the first argument and the condition is the second argument. Go through the field predicates altair documentation and [vega-lite documentation](https://vega.github.io/vega-lite/docs/predicate.html#field-predicate) and use the `FieldOneOfPredicate` for the exercise below.


{:.exercise}
**Exercise** - Use the filter transform to obtain the data related to volcanic activity and earthquake and make an area chart like the one below.

<div id="vis14"></div>
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
    "x": {
      "field": "Year",
      "type": "ordinal"
    },
    "y": {
      "aggregate": "sum",
      "field": "Deaths",
      "type": "quantitative"
    }
  },
  "height": 300,
  "mark": {
    "opacity": 0.8,
    "type": "area"
  },
  "transform": [
    {
      "filter": {
        "field": "Entity",
        "oneOf": [
          "Volcanic activity",
          "Earthquake"
        ]
      }
    }
  ],
  "width": 600
};
  vegaEmbed('#vis14', yourVlSpec);
</script>

<br/>

We now also use the `transform_window()` for data transformation to compute and plot a windowed aggregation of the deaths over all available years.


```R
chart_disasters = alt$Chart("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv")$
  transform_window(
  cumulative_count='sum(Deaths)'
  )$
  mark_area()$
  encode(
    x = 'Year:O',
    y = 'cumulative_count:Q',
    tooltip = c("Year:Q", 'cumulative_count:Q')
  )$transform_filter(
    alt$FieldEqualPredicate(field = "Entity", equal = "All natural disasters")
  )$
  properties(
    height = 300,
    width = 600
  )
```

<div id="vis15"></div>
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
        "type": "quantitative"
      },
      {
        "field": "cumulative_count",
        "type": "quantitative"
      }
    ],
    "x": {
      "field": "Year",
      "type": "ordinal"
    },
    "y": {
      "field": "cumulative_count",
      "type": "quantitative"
    }
  },
  "height": 300,
  "mark": "area",
  "transform": [
    {
      "window": [
        {
          "as": "cumulative_count",
          "field": "Deaths",
          "op": "sum"
        }
      ]
    },
    {
      "filter": {
        "equal": "All natural disasters",
        "field": "Entity"
      }
    }
  ],
  "width": 600
};
  vegaEmbed('#vis15', yourVlSpec);
</script>



{% include custom/series_vega-in-r_next.html %}
