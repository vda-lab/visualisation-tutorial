---
title: Concatenated chart
keywords: vega-in-r
sidebar: vega-in-r_sidebar
permalink: /vega-in-r-concatenated-chart.html
folder: vega-in-r
series: vega-in-r-series
weight: 8
---

To concatenate charts horizontally we can use the `|` operator: `chart_1 | chart_2`.
For vertical concatenation the operator `&` can be used: `chart_1 & chart_2`.
Below, we are combining four charts to create a 2x2 visualisation using `(chart_1 | chart_2) & (chart_3 | chart_4)`.
To specify a title in each plot, we use `title = 'The Title'` inside `$properties()`.

```R
chart_disasters_1 = alt$Chart("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv")$
  mark_line()$
  encode(
    x = 'Year:O',
    y = 'Deaths:Q',
    tooltip = 'Deaths:Q'
  )$
  transform_filter(
    alt$FieldEqualPredicate(field = "Entity", equal = "Landslide")
  )$
  properties(
    width = 400,
    height = 200,
    title = 'Landslide'
  )$
  interactive()

chart_disasters_2 = alt$Chart("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv")$
  mark_line()$
  encode(
    x = 'Year:O',
    y = 'Deaths:Q',
    tooltip = 'Deaths:Q'
  )$
  transform_filter(
    alt$FieldEqualPredicate(field = "Entity", equal = "Volcanic activity")
  )$
  properties(
    width = 400,
    height = 200,
    title = 'Volcanic activity'
  )$
  interactive()

chart_disasters_3 = alt$Chart("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv")$
  mark_line()$
  encode(
    x = 'Year:O',
    y = 'Deaths:Q',
    tooltip = 'Deaths:Q'
  )$
  transform_filter(
    alt$FieldEqualPredicate(field = "Entity", equal = "Wildfire")
  )$
  properties(
    width = 400,
    height = 200,
    title = 'Wildfire'
  )$
  interactive()

chart_disasters_4 = alt$Chart("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv")$
  mark_line()$
  encode(
    x = 'Year:O',
    y = 'Deaths:Q',
    tooltip = 'Deaths:Q'
  )$
  transform_filter(
    alt$FieldEqualPredicate(field = "Entity", equal = "Mass movement (dry)")
  )$
  properties(
    width = 400,
    height = 200,
    title = 'Mass movement (dry)'
  )$
  interactive()

chart_combined = (chart_disasters_1 | chart_disasters_2) & (chart_disasters_3 | chart_disasters_4)
```


<div id="vis18"></div>
<script type="text/javascript">
    var yourVlSpec = {
  "$schema": "https://vega.github.io/schema/vega-lite/v4.0.0.json",
  "config": {
    "view": {
      "continuousHeight": 300,
      "continuousWidth": 400
    }
  },
  "vconcat": [
    {
      "hconcat": [
        {
          "data": {
            "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv"
          },
          "encoding": {
            "tooltip": {
              "field": "Deaths",
              "type": "quantitative"
            },
            "x": {
              "field": "Year",
              "type": "ordinal"
            },
            "y": {
              "field": "Deaths",
              "type": "quantitative"
            }
          },
          "height": 200,
          "mark": "line",
          "selection": {
            "selector014": {
              "bind": "scales",
              "encodings": [
                "x",
                "y"
              ],
              "type": "interval"
            }
          },
          "title": "Landslide",
          "transform": [
            {
              "filter": {
                "equal": "Landslide",
                "field": "Entity"
              }
            }
          ],
          "width": 400
        },
        {
          "data": {
            "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv"
          },
          "encoding": {
            "tooltip": {
              "field": "Deaths",
              "type": "quantitative"
            },
            "x": {
              "field": "Year",
              "type": "ordinal"
            },
            "y": {
              "field": "Deaths",
              "type": "quantitative"
            }
          },
          "height": 200,
          "mark": "line",
          "selection": {
            "selector015": {
              "bind": "scales",
              "encodings": [
                "x",
                "y"
              ],
              "type": "interval"
            }
          },
          "title": "Volcanic activity",
          "transform": [
            {
              "filter": {
                "equal": "Volcanic activity",
                "field": "Entity"
              }
            }
          ],
          "width": 400
        }
      ]
    },
    {
      "hconcat": [
        {
          "data": {
            "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv"
          },
          "encoding": {
            "tooltip": {
              "field": "Deaths",
              "type": "quantitative"
            },
            "x": {
              "field": "Year",
              "type": "ordinal"
            },
            "y": {
              "field": "Deaths",
              "type": "quantitative"
            }
          },
          "height": 200,
          "mark": "line",
          "selection": {
            "selector016": {
              "bind": "scales",
              "encodings": [
                "x",
                "y"
              ],
              "type": "interval"
            }
          },
          "title": "Wildfire",
          "transform": [
            {
              "filter": {
                "equal": "Wildfire",
                "field": "Entity"
              }
            }
          ],
          "width": 400
        },
        {
          "data": {
            "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv"
          },
          "encoding": {
            "tooltip": {
              "field": "Deaths",
              "type": "quantitative"
            },
            "x": {
              "field": "Year",
              "type": "ordinal"
            },
            "y": {
              "field": "Deaths",
              "type": "quantitative"
            }
          },
          "height": 200,
          "mark": "line",
          "selection": {
            "selector017": {
              "bind": "scales",
              "encodings": [
                "x",
                "y"
              ],
              "type": "interval"
            }
          },
          "title": "Mass movement (dry)",
          "transform": [
            {
              "filter": {
                "equal": "Mass movement (dry)",
                "field": "Entity"
              }
            }
          ],
          "width": 400
        }
      ]
    }
  ]
};
  vegaEmbed('#vis18', yourVlSpec);
</script>


{% include custom/series_vega-in-r_next.html %}
