---
title: Layered chart
keywords: vega-in-r
sidebar: vega-in-r_sidebar
permalink: /vega-in-r-layered-chart.html
folder: vega-in-r
series: vega-in-r-series
weight: 7
---

We are now looking at how we can combine charts in one canvas in altair R. This section on how to combine charts, is based on the [View Composition article](https://vegawidget.github.io/altair/articles/view-composition.html).
 
First, we are discussing a layered chart example. Each chart can be made separately and combined uisng the `+` operator: `chart_layer_1 + chart_layer_2`.
Below, we make a chart that consists of a line layer and a point layer. The tooltip should be added to the top layer so that it is visible in the final chart.

```R
chart_disasters_L1 = alt$Chart("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv")$
  mark_line()$
  encode(
    x = 'Year:O',
    y = 'Deaths:Q'
  )$
  transform_filter(
    alt$FieldEqualPredicate(field = "Entity", equal = "All natural disasters")
  )$
  properties(
    height = 400,
    width = 600
  )

chart_disasters_L2 = alt$Chart("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv")$
  mark_point()$
  encode(
    x = 'Year:O',
    y = 'Deaths:Q',
    tooltip = "Deaths:Q"
  )$
  transform_filter(
    alt$FieldEqualPredicate(field = "Entity", equal = "All natural disasters")
  )$
  properties(
    height = 400,
    width = 600
  )

chart_disasters = (chart_disasters_L1 + chart_disasters_L2)
```


<div id="vis16"></div>
<script type="text/javascript">
    var yourVlSpec = {
  "$schema": "https://vega.github.io/schema/vega-lite/v4.0.0.json",
  "config": {
    "view": {
      "continuousHeight": 300,
      "continuousWidth": 400
    }
  },
  "layer": [
    {
      "data": {
        "url": "https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv"
      },
      "encoding": {
        "x": {
          "field": "Year",
          "type": "ordinal"
        },
        "y": {
          "field": "Deaths",
          "type": "quantitative"
        }
      },
      "height": 400,
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
      "height": 400,
      "mark": "point",
      "transform": [
        {
          "filter": {
            "equal": "All natural disasters",
            "field": "Entity"
          }
        }
      ],
      "width": 600
    }
  ]
};
  vegaEmbed('#vis16', yourVlSpec);
</script>

<br/>

To produce the same chart we may also follow the procedure below.
Use the R code provided above for `chart_disasters_L2` and then make the first layer using:

```R
chart_disasters_L1 = chart_disasters_L2$mark_line()
```

Then superimpose the charts as before:
```R
chart_disasters = (chart_disasters_L1 + chart_disasters_L2)
```

{:.exercise}
**Exercise** - Make a layered chart, which consists of one layer for the bar mark and one for the text mark, to produce the chart below.



<div id="vis17"></div>
<script type="text/javascript">
    var yourVlSpec = {
  "$schema": "https://vega.github.io/schema/vega-lite/v4.0.0.json",
  "config": {
    "view": {
      "continuousHeight": 300,
      "continuousWidth": 400
    }
  },
  "datasets": {
    "data-bc4a679881a2f6c12b6dbb818d1a0f16": [
      {
        "Deaths": 1267360,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1900
      },
      {
        "Deaths": 1261000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1900
      },
      {
        "Deaths": 0,
        "Entity": "Earthquake",
        "Missing": "1",
        "Year": 1900
      },
      {
        "Deaths": 30,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1900
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1900
      },
      {
        "Deaths": 6000,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1900
      },
      {
        "Deaths": 300,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1900
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1900
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1900
      },
      {
        "Deaths": 30,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1900
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1900
      },
      {
        "Deaths": 200018,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1901
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1901
      },
      {
        "Deaths": 18,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1901
      },
      {
        "Deaths": 200000,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1901
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1901
      },
      {
        "Deaths": 0,
        "Entity": "Extreme weather",
        "Missing": "1",
        "Year": 1901
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1901
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1901
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1901
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1901
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1901
      },
      {
        "Deaths": 46037,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1902
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1902
      },
      {
        "Deaths": 6747,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1902
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1902
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1902
      },
      {
        "Deaths": 600,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1902
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1902
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1902
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1902
      },
      {
        "Deaths": 38690,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1902
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1902
      },
      {
        "Deaths": 6506,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1903
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1903
      },
      {
        "Deaths": 6000,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1903
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1903
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1903
      },
      {
        "Deaths": 163,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1903
      },
      {
        "Deaths": 250,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1903
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1903
      },
      {
        "Deaths": 76,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1903
      },
      {
        "Deaths": 17,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1903
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1903
      },
      {
        "Deaths": 0,
        "Entity": "All natural disasters",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 0,
        "Entity": "Earthquake",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 0,
        "Entity": "Extreme weather",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1904
      },
      {
        "Deaths": 22758,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1905
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1905
      },
      {
        "Deaths": 22500,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1905
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1905
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1905
      },
      {
        "Deaths": 240,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1905
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1905
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1905
      },
      {
        "Deaths": 18,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1905
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1905
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1905
      },
      {
        "Deaths": 42970,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1906
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1906
      },
      {
        "Deaths": 31966,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1906
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1906
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1906
      },
      {
        "Deaths": 10298,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1906
      },
      {
        "Deaths": 6,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1906
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1906
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1906
      },
      {
        "Deaths": 700,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1906
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1906
      },
      {
        "Deaths": 1325641,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1907
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1907
      },
      {
        "Deaths": 25641,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1907
      },
      {
        "Deaths": 1300000,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1907
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1907
      },
      {
        "Deaths": 0,
        "Entity": "Extreme weather",
        "Missing": "1",
        "Year": 1907
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1907
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1907
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1907
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1907
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1907
      },
      {
        "Deaths": 75033,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1908
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1908
      },
      {
        "Deaths": 75000,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1908
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1908
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1908
      },
      {
        "Deaths": 0,
        "Entity": "Extreme weather",
        "Missing": "1",
        "Year": 1908
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1908
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1908
      },
      {
        "Deaths": 33,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1908
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1908
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1908
      },
      {
        "Deaths": 1511524,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1909
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1909
      },
      {
        "Deaths": 5146,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1909
      },
      {
        "Deaths": 1500040,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1909
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1909
      },
      {
        "Deaths": 713,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1909
      },
      {
        "Deaths": 72,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1909
      },
      {
        "Deaths": 53,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1909
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1909
      },
      {
        "Deaths": 5500,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1909
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1909
      },
      {
        "Deaths": 148233,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1910
      },
      {
        "Deaths": 85000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1910
      },
      {
        "Deaths": 1762,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1910
      },
      {
        "Deaths": 60000,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1910
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1910
      },
      {
        "Deaths": 30,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1910
      },
      {
        "Deaths": 1379,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1910
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1910
      },
      {
        "Deaths": 62,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1910
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1910
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1910
      },
      {
        "Deaths": 102408,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1911
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1911
      },
      {
        "Deaths": 0,
        "Entity": "Earthquake",
        "Missing": "1",
        "Year": 1911
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1911
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1911
      },
      {
        "Deaths": 1000,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1911
      },
      {
        "Deaths": 100000,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1911
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1911
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1911
      },
      {
        "Deaths": 1335,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1911
      },
      {
        "Deaths": 73,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1911
      },
      {
        "Deaths": 52093,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1912
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1912
      },
      {
        "Deaths": 923,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1912
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1912
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1912
      },
      {
        "Deaths": 51170,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1912
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1912
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1912
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1912
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1912
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1912
      },
      {
        "Deaths": 882,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1913
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1913
      },
      {
        "Deaths": 150,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1913
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1913
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1913
      },
      {
        "Deaths": 732,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1913
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1913
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1913
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1913
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1913
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1913
      },
      {
        "Deaths": 289,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1914
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1914
      },
      {
        "Deaths": 149,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1914
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1914
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1914
      },
      {
        "Deaths": 0,
        "Entity": "Extreme weather",
        "Missing": "1",
        "Year": 1914
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1914
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1914
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1914
      },
      {
        "Deaths": 140,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1914
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1914
      },
      {
        "Deaths": 32167,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1915
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1915
      },
      {
        "Deaths": 29986,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1915
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1915
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1915
      },
      {
        "Deaths": 2125,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1915
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1915
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1915
      },
      {
        "Deaths": 56,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1915
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1915
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1915
      },
      {
        "Deaths": 300,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1916
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1916
      },
      {
        "Deaths": 0,
        "Entity": "Earthquake",
        "Missing": "1",
        "Year": 1916
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1916
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1916
      },
      {
        "Deaths": 300,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1916
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1916
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1916
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1916
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1916
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1916
      },
      {
        "Deaths": 2523507,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1917
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1917
      },
      {
        "Deaths": 19450,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1917
      },
      {
        "Deaths": 2500000,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1917
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1917
      },
      {
        "Deaths": 4057,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1917
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1917
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1917
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1917
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1917
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1917
      },
      {
        "Deaths": 461113,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1918
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1918
      },
      {
        "Deaths": 10379,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1918
      },
      {
        "Deaths": 449700,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1918
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1918
      },
      {
        "Deaths": 34,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1918
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1918
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1918
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1918
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1918
      },
      {
        "Deaths": 1000,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1918
      },
      {
        "Deaths": 5500,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1919
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1919
      },
      {
        "Deaths": 0,
        "Entity": "Earthquake",
        "Missing": "1",
        "Year": 1919
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1919
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1919
      },
      {
        "Deaths": 500,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1919
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1919
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1919
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1919
      },
      {
        "Deaths": 5000,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1919
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1919
      },
      {
        "Deaths": 3204224,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1920
      },
      {
        "Deaths": 524000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1920
      },
      {
        "Deaths": 180000,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1920
      },
      {
        "Deaths": 2500000,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1920
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1920
      },
      {
        "Deaths": 224,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1920
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1920
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1920
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1920
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1920
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1920
      },
      {
        "Deaths": 1200000,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1921
      },
      {
        "Deaths": 1200000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1921
      },
      {
        "Deaths": 0,
        "Entity": "Earthquake",
        "Missing": "1",
        "Year": 1921
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1921
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1921
      },
      {
        "Deaths": 0,
        "Entity": "Extreme weather",
        "Missing": "1",
        "Year": 1921
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1921
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1921
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1921
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1921
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1921
      },
      {
        "Deaths": 101243,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1922
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1922
      },
      {
        "Deaths": 1100,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1922
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1922
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1922
      },
      {
        "Deaths": 100000,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1922
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1922
      },
      {
        "Deaths": 100,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1922
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1922
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1922
      },
      {
        "Deaths": 43,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1922
      },
      {
        "Deaths": 255701,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1923
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1923
      },
      {
        "Deaths": 152362,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1923
      },
      {
        "Deaths": 100000,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1923
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1923
      },
      {
        "Deaths": 3139,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1923
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1923
      },
      {
        "Deaths": 200,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1923
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1923
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1923
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1923
      },
      {
        "Deaths": 303009,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1924
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1924
      },
      {
        "Deaths": 767,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1924
      },
      {
        "Deaths": 300000,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1924
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1924
      },
      {
        "Deaths": 2242,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1924
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1924
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1924
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1924
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1924
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1924
      },
      {
        "Deaths": 5832,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1925
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1925
      },
      {
        "Deaths": 5013,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1925
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1925
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1925
      },
      {
        "Deaths": 819,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1925
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1925
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1925
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1925
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1925
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1925
      },
      {
        "Deaths": 427852,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1926
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1926
      },
      {
        "Deaths": 12,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1926
      },
      {
        "Deaths": 423000,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1926
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1926
      },
      {
        "Deaths": 3568,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1926
      },
      {
        "Deaths": 1000,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1926
      },
      {
        "Deaths": 128,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1926
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1926
      },
      {
        "Deaths": 144,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1926
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1926
      },
      {
        "Deaths": 215160,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1927
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1927
      },
      {
        "Deaths": 206142,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1927
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1927
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1927
      },
      {
        "Deaths": 5772,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1927
      },
      {
        "Deaths": 3246,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1927
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1927
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1927
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1927
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1927
      },
      {
        "Deaths": 3004895,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1928
      },
      {
        "Deaths": 3000000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1928
      },
      {
        "Deaths": 635,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1928
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1928
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1928
      },
      {
        "Deaths": 4224,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1928
      },
      {
        "Deaths": 36,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1928
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1928
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1928
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1928
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1928
      },
      {
        "Deaths": 8377,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1929
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1929
      },
      {
        "Deaths": 3317,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1929
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1929
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1929
      },
      {
        "Deaths": 0,
        "Entity": "Extreme weather",
        "Missing": "1",
        "Year": 1929
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1929
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1929
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1929
      },
      {
        "Deaths": 5000,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1929
      },
      {
        "Deaths": 60,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1929
      },
      {
        "Deaths": 10572,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1930
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1930
      },
      {
        "Deaths": 5081,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1930
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1930
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1930
      },
      {
        "Deaths": 4082,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1930
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1930
      },
      {
        "Deaths": 40,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1930
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1930
      },
      {
        "Deaths": 1369,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1930
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1930
      },
      {
        "Deaths": 3706227,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1931
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1931
      },
      {
        "Deaths": 1537,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1931
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1931
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1931
      },
      {
        "Deaths": 3200,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1931
      },
      {
        "Deaths": 3700000,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1931
      },
      {
        "Deaths": 190,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1931
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1931
      },
      {
        "Deaths": 1300,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1931
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1931
      },
      {
        "Deaths": 73296,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1932
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1932
      },
      {
        "Deaths": 70006,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1932
      },
      {
        "Deaths": 16,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1932
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1932
      },
      {
        "Deaths": 3244,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1932
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1932
      },
      {
        "Deaths": 30,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1932
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1932
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1932
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1932
      },
      {
        "Deaths": 34296,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1933
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1933
      },
      {
        "Deaths": 16180,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1933
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1933
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1933
      },
      {
        "Deaths": 63,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1933
      },
      {
        "Deaths": 18053,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1933
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1933
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1933
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1933
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1933
      },
      {
        "Deaths": 21087,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1934
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1934
      },
      {
        "Deaths": 15496,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1934
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1934
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1934
      },
      {
        "Deaths": 5091,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1934
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1934
      },
      {
        "Deaths": 500,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1934
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1934
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1934
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1934
      },
      {
        "Deaths": 272817,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1935
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1935
      },
      {
        "Deaths": 66110,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1935
      },
      {
        "Deaths": 2000,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1935
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1935
      },
      {
        "Deaths": 62707,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1935
      },
      {
        "Deaths": 142000,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1935
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1935
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1935
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1935
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1935
      },
      {
        "Deaths": 5301,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1936
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1936
      },
      {
        "Deaths": 26,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1936
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1936
      },
      {
        "Deaths": 1693,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1936
      },
      {
        "Deaths": 3309,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1936
      },
      {
        "Deaths": 200,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1936
      },
      {
        "Deaths": 73,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1936
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1936
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1936
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1936
      },
      {
        "Deaths": 12025,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1937
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1937
      },
      {
        "Deaths": 0,
        "Entity": "Earthquake",
        "Missing": "1",
        "Year": 1937
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1937
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1937
      },
      {
        "Deaths": 11231,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1937
      },
      {
        "Deaths": 248,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1937
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1937
      },
      {
        "Deaths": 40,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1937
      },
      {
        "Deaths": 506,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1937
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1937
      },
      {
        "Deaths": 2225,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1938
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1938
      },
      {
        "Deaths": 166,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1938
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1938
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1938
      },
      {
        "Deaths": 905,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1938
      },
      {
        "Deaths": 954,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1938
      },
      {
        "Deaths": 200,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1938
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1938
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1938
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1938
      },
      {
        "Deaths": 563178,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1939
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1939
      },
      {
        "Deaths": 63094,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1939
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1939
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1939
      },
      {
        "Deaths": 3,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1939
      },
      {
        "Deaths": 500010,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1939
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1939
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1939
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1939
      },
      {
        "Deaths": 71,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1939
      },
      {
        "Deaths": 23023,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1940
      },
      {
        "Deaths": 20000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1940
      },
      {
        "Deaths": 1275,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1940
      },
      {
        "Deaths": 1500,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1940
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1940
      },
      {
        "Deaths": 123,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1940
      },
      {
        "Deaths": 125,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1940
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1940
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1940
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1940
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1940
      },
      {
        "Deaths": 10195,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1941
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1941
      },
      {
        "Deaths": 189,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1941
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1941
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1941
      },
      {
        "Deaths": 5006,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1941
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1941
      },
      {
        "Deaths": 5000,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1941
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1941
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1941
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1941
      },
      {
        "Deaths": 1608235,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1942
      },
      {
        "Deaths": 1500000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1942
      },
      {
        "Deaths": 7235,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1942
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1942
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1942
      },
      {
        "Deaths": 101000,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1942
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1942
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1942
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1942
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1942
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1942
      },
      {
        "Deaths": 1910322,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1943
      },
      {
        "Deaths": 1900000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1943
      },
      {
        "Deaths": 4332,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1943
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1943
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1943
      },
      {
        "Deaths": 5000,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1943
      },
      {
        "Deaths": 990,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1943
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1943
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1943
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1943
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1943
      },
      {
        "Deaths": 15906,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1944
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1944
      },
      {
        "Deaths": 14984,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1944
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1944
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1944
      },
      {
        "Deaths": 726,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1944
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1944
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1944
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1944
      },
      {
        "Deaths": 26,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1944
      },
      {
        "Deaths": 170,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1944
      },
      {
        "Deaths": 10376,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1945
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1945
      },
      {
        "Deaths": 5961,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1945
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1945
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1945
      },
      {
        "Deaths": 4415,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1945
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1945
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1945
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1945
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1945
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1945
      },
      {
        "Deaths": 35490,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1946
      },
      {
        "Deaths": 30000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1946
      },
      {
        "Deaths": 5153,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1946
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1946
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1946
      },
      {
        "Deaths": 337,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1946
      },
      {
        "Deaths": 0,
        "Entity": "Flood",
        "Missing": "1",
        "Year": 1946
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1946
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1946
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1946
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1946
      },
      {
        "Deaths": 17647,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1947
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1947
      },
      {
        "Deaths": 633,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1947
      },
      {
        "Deaths": 10276,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1947
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1947
      },
      {
        "Deaths": 4738,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1947
      },
      {
        "Deaths": 2000,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1947
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1947
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1947
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1947
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1947
      },
      {
        "Deaths": 120131,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1948
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1948
      },
      {
        "Deaths": 115618,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1948
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1948
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1948
      },
      {
        "Deaths": 2971,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1948
      },
      {
        "Deaths": 917,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1948
      },
      {
        "Deaths": 525,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1948
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1948
      },
      {
        "Deaths": 100,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1948
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1948
      },
      {
        "Deaths": 120370,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1949
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1949
      },
      {
        "Deaths": 6486,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1949
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1949
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1949
      },
      {
        "Deaths": 2804,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1949
      },
      {
        "Deaths": 97000,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1949
      },
      {
        "Deaths": 12000,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1949
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1949
      },
      {
        "Deaths": 2000,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1949
      },
      {
        "Deaths": 80,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1949
      },
      {
        "Deaths": 6728,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1950
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1950
      },
      {
        "Deaths": 1833,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1950
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1950
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1950
      },
      {
        "Deaths": 873,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1950
      },
      {
        "Deaths": 3808,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1950
      },
      {
        "Deaths": 130,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1950
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1950
      },
      {
        "Deaths": 84,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1950
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1950
      },
      {
        "Deaths": 15042,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1951
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1951
      },
      {
        "Deaths": 1554,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1951
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1951
      },
      {
        "Deaths": 69,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1951
      },
      {
        "Deaths": 2861,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1951
      },
      {
        "Deaths": 5666,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1951
      },
      {
        "Deaths": 92,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1951
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1951
      },
      {
        "Deaths": 4800,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1951
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1951
      },
      {
        "Deaths": 8965,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1952
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1952
      },
      {
        "Deaths": 2432,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1952
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1952
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1952
      },
      {
        "Deaths": 6277,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1952
      },
      {
        "Deaths": 199,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1952
      },
      {
        "Deaths": 28,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1952
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1952
      },
      {
        "Deaths": 29,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1952
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1952
      },
      {
        "Deaths": 12956,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1953
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1953
      },
      {
        "Deaths": 2717,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1953
      },
      {
        "Deaths": 481,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1953
      },
      {
        "Deaths": 669,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1953
      },
      {
        "Deaths": 1814,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1953
      },
      {
        "Deaths": 7125,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1953
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1953
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1953
      },
      {
        "Deaths": 150,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1953
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1953
      },
      {
        "Deaths": 41872,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1954
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1954
      },
      {
        "Deaths": 3344,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1954
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1954
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1954
      },
      {
        "Deaths": 2969,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1954
      },
      {
        "Deaths": 34436,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1954
      },
      {
        "Deaths": 1086,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1954
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1954
      },
      {
        "Deaths": 37,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1954
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1954
      },
      {
        "Deaths": 6026,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1955
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1955
      },
      {
        "Deaths": 959,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1955
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1955
      },
      {
        "Deaths": 107,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1955
      },
      {
        "Deaths": 3895,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1955
      },
      {
        "Deaths": 584,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1955
      },
      {
        "Deaths": 478,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1955
      },
      {
        "Deaths": 3,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1955
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1955
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1955
      },
      {
        "Deaths": 7737,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1956
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1956
      },
      {
        "Deaths": 763,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1956
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1956
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1956
      },
      {
        "Deaths": 3114,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1956
      },
      {
        "Deaths": 3613,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1956
      },
      {
        "Deaths": 236,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1956
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1956
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1956
      },
      {
        "Deaths": 11,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1956
      },
      {
        "Deaths": 10603,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1957
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1957
      },
      {
        "Deaths": 6993,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1957
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1957
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1957
      },
      {
        "Deaths": 1139,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1957
      },
      {
        "Deaths": 2471,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1957
      },
      {
        "Deaths": 0,
        "Entity": "Landslide",
        "Missing": "1",
        "Year": 1957
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1957
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1957
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1957
      },
      {
        "Deaths": 3950,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1958
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1958
      },
      {
        "Deaths": 227,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1958
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1958
      },
      {
        "Deaths": 651,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1958
      },
      {
        "Deaths": 2620,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1958
      },
      {
        "Deaths": 400,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1958
      },
      {
        "Deaths": 52,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1958
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1958
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1958
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1958
      },
      {
        "Deaths": 2013242,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1959
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1959
      },
      {
        "Deaths": 103,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1959
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1959
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1959
      },
      {
        "Deaths": 9695,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1959
      },
      {
        "Deaths": 2003396,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1959
      },
      {
        "Deaths": 48,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1959
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1959
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1959
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1959
      },
      {
        "Deaths": 39188,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1960
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1960
      },
      {
        "Deaths": 19395,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1960
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1960
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1960
      },
      {
        "Deaths": 9164,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1960
      },
      {
        "Deaths": 10577,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1960
      },
      {
        "Deaths": 52,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1960
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1960
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1960
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1960
      },
      {
        "Deaths": 17341,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1961
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1961
      },
      {
        "Deaths": 60,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1961
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1961
      },
      {
        "Deaths": 400,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1961
      },
      {
        "Deaths": 12852,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1961
      },
      {
        "Deaths": 3863,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1961
      },
      {
        "Deaths": 166,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1961
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1961
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1961
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1961
      },
      {
        "Deaths": 17370,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1962
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1962
      },
      {
        "Deaths": 12209,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1962
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1962
      },
      {
        "Deaths": 50,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1962
      },
      {
        "Deaths": 1860,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1962
      },
      {
        "Deaths": 1180,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1962
      },
      {
        "Deaths": 71,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1962
      },
      {
        "Deaths": 2000,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1962
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1962
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1962
      },
      {
        "Deaths": 37746,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1963
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1963
      },
      {
        "Deaths": 1700,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1963
      },
      {
        "Deaths": 1000,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1963
      },
      {
        "Deaths": 162,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1963
      },
      {
        "Deaths": 29965,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1963
      },
      {
        "Deaths": 1031,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1963
      },
      {
        "Deaths": 2033,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1963
      },
      {
        "Deaths": 150,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1963
      },
      {
        "Deaths": 1705,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1963
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1963
      },
      {
        "Deaths": 12892,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1964
      },
      {
        "Deaths": 50,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1964
      },
      {
        "Deaths": 335,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1964
      },
      {
        "Deaths": 617,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1964
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1964
      },
      {
        "Deaths": 10655,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1964
      },
      {
        "Deaths": 1123,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1964
      },
      {
        "Deaths": 108,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1964
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1964
      },
      {
        "Deaths": 4,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1964
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1964
      },
      {
        "Deaths": 1565517,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 1502000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 683,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 816,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 100,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 59932,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 1401,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 204,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 26,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 355,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1965
      },
      {
        "Deaths": 17181,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1966
      },
      {
        "Deaths": 8000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1966
      },
      {
        "Deaths": 2752,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1966
      },
      {
        "Deaths": 200,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1966
      },
      {
        "Deaths": 262,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1966
      },
      {
        "Deaths": 2327,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1966
      },
      {
        "Deaths": 1923,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1966
      },
      {
        "Deaths": 604,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1966
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1966
      },
      {
        "Deaths": 1088,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1966
      },
      {
        "Deaths": 25,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1966
      },
      {
        "Deaths": 10103,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1967
      },
      {
        "Deaths": 600,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1967
      },
      {
        "Deaths": 1013,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1967
      },
      {
        "Deaths": 3137,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1967
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1967
      },
      {
        "Deaths": 2255,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1967
      },
      {
        "Deaths": 2446,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1967
      },
      {
        "Deaths": 590,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1967
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1967
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1967
      },
      {
        "Deaths": 62,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1967
      },
      {
        "Deaths": 21461,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1968
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1968
      },
      {
        "Deaths": 10858,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1968
      },
      {
        "Deaths": 177,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1968
      },
      {
        "Deaths": 153,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1968
      },
      {
        "Deaths": 1669,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1968
      },
      {
        "Deaths": 7306,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1968
      },
      {
        "Deaths": 1196,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1968
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1968
      },
      {
        "Deaths": 90,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1968
      },
      {
        "Deaths": 12,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1968
      },
      {
        "Deaths": 11687,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1969
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1969
      },
      {
        "Deaths": 3353,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1969
      },
      {
        "Deaths": 3520,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1969
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1969
      },
      {
        "Deaths": 3252,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1969
      },
      {
        "Deaths": 1544,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1969
      },
      {
        "Deaths": 18,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1969
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1969
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1969
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1969
      },
      {
        "Deaths": 387507,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1970
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1970
      },
      {
        "Deaths": 78599,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1970
      },
      {
        "Deaths": 939,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1970
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1970
      },
      {
        "Deaths": 304495,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1970
      },
      {
        "Deaths": 3246,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1970
      },
      {
        "Deaths": 186,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1970
      },
      {
        "Deaths": 42,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1970
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1970
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1970
      },
      {
        "Deaths": 18086,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1971
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1971
      },
      {
        "Deaths": 1107,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1971
      },
      {
        "Deaths": 2313,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1971
      },
      {
        "Deaths": 400,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1971
      },
      {
        "Deaths": 10811,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1971
      },
      {
        "Deaths": 2404,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1971
      },
      {
        "Deaths": 1020,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1971
      },
      {
        "Deaths": 31,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1971
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1971
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1971
      },
      {
        "Deaths": 20045,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1972
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1972
      },
      {
        "Deaths": 15170,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1972
      },
      {
        "Deaths": 35,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1972
      },
      {
        "Deaths": 110,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1972
      },
      {
        "Deaths": 1427,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1972
      },
      {
        "Deaths": 2548,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1972
      },
      {
        "Deaths": 755,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1972
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1972
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1972
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1972
      },
      {
        "Deaths": 110555,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1973
      },
      {
        "Deaths": 100000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1973
      },
      {
        "Deaths": 552,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1973
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1973
      },
      {
        "Deaths": 283,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1973
      },
      {
        "Deaths": 4344,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1973
      },
      {
        "Deaths": 1835,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1973
      },
      {
        "Deaths": 3541,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1973
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1973
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1973
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1973
      },
      {
        "Deaths": 87504,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1974
      },
      {
        "Deaths": 19000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1974
      },
      {
        "Deaths": 24808,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1974
      },
      {
        "Deaths": 1500,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1974
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1974
      },
      {
        "Deaths": 11861,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1974
      },
      {
        "Deaths": 29431,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1974
      },
      {
        "Deaths": 904,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1974
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1974
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1974
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1974
      },
      {
        "Deaths": 14858,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1975
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1975
      },
      {
        "Deaths": 12632,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1975
      },
      {
        "Deaths": 0,
        "Entity": "Epidemic",
        "Missing": "1",
        "Year": 1975
      },
      {
        "Deaths": 140,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1975
      },
      {
        "Deaths": 1041,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1975
      },
      {
        "Deaths": 848,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1975
      },
      {
        "Deaths": 195,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1975
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1975
      },
      {
        "Deaths": 2,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1975
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1975
      },
      {
        "Deaths": 280469,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1976
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1976
      },
      {
        "Deaths": 276994,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1976
      },
      {
        "Deaths": 396,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1976
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1976
      },
      {
        "Deaths": 1763,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1976
      },
      {
        "Deaths": 960,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1976
      },
      {
        "Deaths": 315,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1976
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1976
      },
      {
        "Deaths": 41,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1976
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1976
      },
      {
        "Deaths": 22406,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1977
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1977
      },
      {
        "Deaths": 3098,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1977
      },
      {
        "Deaths": 1184,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1977
      },
      {
        "Deaths": 0,
        "Entity": "Extreme temperature",
        "Missing": "1",
        "Year": 1977
      },
      {
        "Deaths": 15298,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1977
      },
      {
        "Deaths": 2568,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1977
      },
      {
        "Deaths": 40,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1977
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1977
      },
      {
        "Deaths": 215,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1977
      },
      {
        "Deaths": 3,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1977
      },
      {
        "Deaths": 38096,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1978
      },
      {
        "Deaths": 63,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1978
      },
      {
        "Deaths": 25162,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1978
      },
      {
        "Deaths": 3060,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1978
      },
      {
        "Deaths": 150,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1978
      },
      {
        "Deaths": 3676,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1978
      },
      {
        "Deaths": 5897,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1978
      },
      {
        "Deaths": 86,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1978
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1978
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1978
      },
      {
        "Deaths": 2,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1978
      },
      {
        "Deaths": 7341,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1979
      },
      {
        "Deaths": 18,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1979
      },
      {
        "Deaths": 2100,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1979
      },
      {
        "Deaths": 486,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1979
      },
      {
        "Deaths": 470,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1979
      },
      {
        "Deaths": 2623,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1979
      },
      {
        "Deaths": 1038,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1979
      },
      {
        "Deaths": 338,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1979
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1979
      },
      {
        "Deaths": 268,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1979
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1979
      },
      {
        "Deaths": 23089,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1980
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1980
      },
      {
        "Deaths": 7730,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1980
      },
      {
        "Deaths": 1685,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1980
      },
      {
        "Deaths": 1389,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1980
      },
      {
        "Deaths": 1379,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1980
      },
      {
        "Deaths": 10466,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1980
      },
      {
        "Deaths": 300,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1980
      },
      {
        "Deaths": 50,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1980
      },
      {
        "Deaths": 90,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1980
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1980
      },
      {
        "Deaths": 119697,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1981
      },
      {
        "Deaths": 103000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1981
      },
      {
        "Deaths": 4206,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1981
      },
      {
        "Deaths": 2497,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1981
      },
      {
        "Deaths": 300,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1981
      },
      {
        "Deaths": 3790,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1981
      },
      {
        "Deaths": 5283,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1981
      },
      {
        "Deaths": 421,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1981
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1981
      },
      {
        "Deaths": 192,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1981
      },
      {
        "Deaths": 8,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1981
      },
      {
        "Deaths": 13973,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 280,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 2120,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 2912,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 400,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 2782,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 4648,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 640,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 59,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 130,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 2,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1982
      },
      {
        "Deaths": 461561,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1983
      },
      {
        "Deaths": 450520,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1983
      },
      {
        "Deaths": 2148,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1983
      },
      {
        "Deaths": 1219,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1983
      },
      {
        "Deaths": 205,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1983
      },
      {
        "Deaths": 3656,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1983
      },
      {
        "Deaths": 2082,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1983
      },
      {
        "Deaths": 1159,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1983
      },
      {
        "Deaths": 466,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1983
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1983
      },
      {
        "Deaths": 106,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1983
      },
      {
        "Deaths": 16273,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1984
      },
      {
        "Deaths": 230,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1984
      },
      {
        "Deaths": 57,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1984
      },
      {
        "Deaths": 7016,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1984
      },
      {
        "Deaths": 290,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1984
      },
      {
        "Deaths": 5468,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1984
      },
      {
        "Deaths": 2930,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1984
      },
      {
        "Deaths": 228,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1984
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1984
      },
      {
        "Deaths": 37,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1984
      },
      {
        "Deaths": 17,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1984
      },
      {
        "Deaths": 60232,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1985
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1985
      },
      {
        "Deaths": 9853,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1985
      },
      {
        "Deaths": 5854,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1985
      },
      {
        "Deaths": 456,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1985
      },
      {
        "Deaths": 17165,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1985
      },
      {
        "Deaths": 4376,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1985
      },
      {
        "Deaths": 377,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1985
      },
      {
        "Deaths": 300,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1985
      },
      {
        "Deaths": 21800,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1985
      },
      {
        "Deaths": 51,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1985
      },
      {
        "Deaths": 10349,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1986
      },
      {
        "Deaths": 84,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1986
      },
      {
        "Deaths": 1181,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1986
      },
      {
        "Deaths": 3046,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1986
      },
      {
        "Deaths": 50,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1986
      },
      {
        "Deaths": 1939,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1986
      },
      {
        "Deaths": 1782,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1986
      },
      {
        "Deaths": 501,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1986
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1986
      },
      {
        "Deaths": 1746,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1986
      },
      {
        "Deaths": 20,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1986
      },
      {
        "Deaths": 21533,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1987
      },
      {
        "Deaths": 1317,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1987
      },
      {
        "Deaths": 5160,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1987
      },
      {
        "Deaths": 2592,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1987
      },
      {
        "Deaths": 1220,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1987
      },
      {
        "Deaths": 2900,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1987
      },
      {
        "Deaths": 6766,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1987
      },
      {
        "Deaths": 1204,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1987
      },
      {
        "Deaths": 183,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1987
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1987
      },
      {
        "Deaths": 191,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1987
      },
      {
        "Deaths": 57464,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1988
      },
      {
        "Deaths": 1600,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1988
      },
      {
        "Deaths": 27049,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1988
      },
      {
        "Deaths": 15216,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1988
      },
      {
        "Deaths": 644,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1988
      },
      {
        "Deaths": 3335,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1988
      },
      {
        "Deaths": 8504,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1988
      },
      {
        "Deaths": 952,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1988
      },
      {
        "Deaths": 157,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1988
      },
      {
        "Deaths": 7,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1988
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1988
      },
      {
        "Deaths": 12611,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1989
      },
      {
        "Deaths": 237,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1989
      },
      {
        "Deaths": 650,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1989
      },
      {
        "Deaths": 1870,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1989
      },
      {
        "Deaths": 381,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1989
      },
      {
        "Deaths": 4256,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1989
      },
      {
        "Deaths": 4716,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1989
      },
      {
        "Deaths": 445,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1989
      },
      {
        "Deaths": 55,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1989
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1989
      },
      {
        "Deaths": 1,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1989
      },
      {
        "Deaths": 53141,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1990
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1990
      },
      {
        "Deaths": 42853,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1990
      },
      {
        "Deaths": 2207,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1990
      },
      {
        "Deaths": 979,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1990
      },
      {
        "Deaths": 4604,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1990
      },
      {
        "Deaths": 2251,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1990
      },
      {
        "Deaths": 98,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1990
      },
      {
        "Deaths": 116,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1990
      },
      {
        "Deaths": 33,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1990
      },
      {
        "Deaths": 0,
        "Entity": "Wildfire",
        "Missing": "1",
        "Year": 1990
      },
      {
        "Deaths": 189707,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 2000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 2454,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 30682,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 835,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 146297,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 5852,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 728,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 86,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 683,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 90,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1991
      },
      {
        "Deaths": 18911,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1992
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1992
      },
      {
        "Deaths": 4033,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1992
      },
      {
        "Deaths": 6675,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1992
      },
      {
        "Deaths": 388,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1992
      },
      {
        "Deaths": 1342,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1992
      },
      {
        "Deaths": 5315,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1992
      },
      {
        "Deaths": 712,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1992
      },
      {
        "Deaths": 323,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1992
      },
      {
        "Deaths": 1,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1992
      },
      {
        "Deaths": 122,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1992
      },
      {
        "Deaths": 21821,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1993
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1993
      },
      {
        "Deaths": 10088,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1993
      },
      {
        "Deaths": 651,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1993
      },
      {
        "Deaths": 106,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1993
      },
      {
        "Deaths": 2965,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1993
      },
      {
        "Deaths": 6150,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1993
      },
      {
        "Deaths": 1418,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1993
      },
      {
        "Deaths": 341,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 1993
      },
      {
        "Deaths": 99,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1993
      },
      {
        "Deaths": 3,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1993
      },
      {
        "Deaths": 15590,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1994
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1994
      },
      {
        "Deaths": 1242,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1994
      },
      {
        "Deaths": 2505,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1994
      },
      {
        "Deaths": 341,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1994
      },
      {
        "Deaths": 4239,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1994
      },
      {
        "Deaths": 6771,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1994
      },
      {
        "Deaths": 307,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1994
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1994
      },
      {
        "Deaths": 101,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1994
      },
      {
        "Deaths": 84,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1994
      },
      {
        "Deaths": 27166,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1995
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1995
      },
      {
        "Deaths": 7739,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1995
      },
      {
        "Deaths": 4428,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1995
      },
      {
        "Deaths": 1730,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1995
      },
      {
        "Deaths": 3763,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1995
      },
      {
        "Deaths": 7956,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1995
      },
      {
        "Deaths": 1521,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1995
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1995
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1995
      },
      {
        "Deaths": 29,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1995
      },
      {
        "Deaths": 31595,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1996
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 1996
      },
      {
        "Deaths": 576,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1996
      },
      {
        "Deaths": 16887,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1996
      },
      {
        "Deaths": 300,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1996
      },
      {
        "Deaths": 4581,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1996
      },
      {
        "Deaths": 8047,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1996
      },
      {
        "Deaths": 1155,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1996
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1996
      },
      {
        "Deaths": 4,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1996
      },
      {
        "Deaths": 45,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1996
      },
      {
        "Deaths": 30124,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1997
      },
      {
        "Deaths": 732,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1997
      },
      {
        "Deaths": 3159,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1997
      },
      {
        "Deaths": 10674,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1997
      },
      {
        "Deaths": 604,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1997
      },
      {
        "Deaths": 6150,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1997
      },
      {
        "Deaths": 7685,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1997
      },
      {
        "Deaths": 801,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1997
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1997
      },
      {
        "Deaths": 53,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 1997
      },
      {
        "Deaths": 266,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1997
      },
      {
        "Deaths": 62672,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1998
      },
      {
        "Deaths": 20,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1998
      },
      {
        "Deaths": 9573,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1998
      },
      {
        "Deaths": 12931,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1998
      },
      {
        "Deaths": 3269,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1998
      },
      {
        "Deaths": 24935,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1998
      },
      {
        "Deaths": 10653,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1998
      },
      {
        "Deaths": 1141,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1998
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1998
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1998
      },
      {
        "Deaths": 150,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1998
      },
      {
        "Deaths": 76886,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1999
      },
      {
        "Deaths": 361,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 1999
      },
      {
        "Deaths": 21869,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 1999
      },
      {
        "Deaths": 6293,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 1999
      },
      {
        "Deaths": 771,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 1999
      },
      {
        "Deaths": 12270,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 1999
      },
      {
        "Deaths": 34807,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 1999
      },
      {
        "Deaths": 445,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 1999
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 1999
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 1999
      },
      {
        "Deaths": 70,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 1999
      },
      {
        "Deaths": 16667,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2000
      },
      {
        "Deaths": 80,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 2000
      },
      {
        "Deaths": 217,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2000
      },
      {
        "Deaths": 6980,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2000
      },
      {
        "Deaths": 941,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2000
      },
      {
        "Deaths": 1354,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2000
      },
      {
        "Deaths": 6025,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2000
      },
      {
        "Deaths": 1012,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2000
      },
      {
        "Deaths": 11,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 2000
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 2000
      },
      {
        "Deaths": 47,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2000
      },
      {
        "Deaths": 39493,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2001
      },
      {
        "Deaths": 99,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 2001
      },
      {
        "Deaths": 21348,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2001
      },
      {
        "Deaths": 8515,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2001
      },
      {
        "Deaths": 1787,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2001
      },
      {
        "Deaths": 1911,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2001
      },
      {
        "Deaths": 5014,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2001
      },
      {
        "Deaths": 786,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2001
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 2001
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 2001
      },
      {
        "Deaths": 33,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2001
      },
      {
        "Deaths": 21342,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 588,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 1639,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 8762,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 3369,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 1382,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 4236,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 1100,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 60,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 200,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 6,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2002
      },
      {
        "Deaths": 113558,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2003
      },
      {
        "Deaths": 9,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 2003
      },
      {
        "Deaths": 29617,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2003
      },
      {
        "Deaths": 3522,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2003
      },
      {
        "Deaths": 74698,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2003
      },
      {
        "Deaths": 1049,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2003
      },
      {
        "Deaths": 3910,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2003
      },
      {
        "Deaths": 706,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2003
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 2003
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 2003
      },
      {
        "Deaths": 47,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2003
      },
      {
        "Deaths": 244772,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 80,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 227290,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 3245,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 255,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 6547,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 6982,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 313,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 44,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 2,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 14,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2004
      },
      {
        "Deaths": 93566,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2005
      },
      {
        "Deaths": 149,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 2005
      },
      {
        "Deaths": 76241,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2005
      },
      {
        "Deaths": 3909,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2005
      },
      {
        "Deaths": 1550,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2005
      },
      {
        "Deaths": 5251,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2005
      },
      {
        "Deaths": 5754,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2005
      },
      {
        "Deaths": 664,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2005
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 2005
      },
      {
        "Deaths": 3,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 2005
      },
      {
        "Deaths": 45,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2005
      },
      {
        "Deaths": 29893,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 134,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 6692,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 6402,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 4826,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 4329,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 5843,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 1638,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 11,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 5,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 13,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2006
      },
      {
        "Deaths": 22422,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2007
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 2007
      },
      {
        "Deaths": 780,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2007
      },
      {
        "Deaths": 5484,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2007
      },
      {
        "Deaths": 1086,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2007
      },
      {
        "Deaths": 6035,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2007
      },
      {
        "Deaths": 8607,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2007
      },
      {
        "Deaths": 271,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2007
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 2007
      },
      {
        "Deaths": 11,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 2007
      },
      {
        "Deaths": 148,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2007
      },
      {
        "Deaths": 242236,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 8,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 87918,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 6904,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 1688,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 140985,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 4007,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 504,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 120,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 16,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 86,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2008
      },
      {
        "Deaths": 16037,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2009
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 2009
      },
      {
        "Deaths": 1893,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2009
      },
      {
        "Deaths": 4895,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2009
      },
      {
        "Deaths": 1386,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2009
      },
      {
        "Deaths": 3287,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2009
      },
      {
        "Deaths": 3627,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2009
      },
      {
        "Deaths": 723,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2009
      },
      {
        "Deaths": 36,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 2009
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 2009
      },
      {
        "Deaths": 190,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2009
      },
      {
        "Deaths": 329900,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2010
      },
      {
        "Deaths": 20000,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 2010
      },
      {
        "Deaths": 226733,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2010
      },
      {
        "Deaths": 12143,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2010
      },
      {
        "Deaths": 57188,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2010
      },
      {
        "Deaths": 1564,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2010
      },
      {
        "Deaths": 8356,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2010
      },
      {
        "Deaths": 3427,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2010
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 2010
      },
      {
        "Deaths": 323,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 2010
      },
      {
        "Deaths": 166,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2010
      },
      {
        "Deaths": 34143,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2011
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 2011
      },
      {
        "Deaths": 20946,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2011
      },
      {
        "Deaths": 3174,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2011
      },
      {
        "Deaths": 435,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2011
      },
      {
        "Deaths": 3103,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2011
      },
      {
        "Deaths": 6163,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2011
      },
      {
        "Deaths": 309,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2011
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 2011
      },
      {
        "Deaths": 3,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 2011
      },
      {
        "Deaths": 10,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2011
      },
      {
        "Deaths": 11619,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2012
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 2012
      },
      {
        "Deaths": 711,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2012
      },
      {
        "Deaths": 1887,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2012
      },
      {
        "Deaths": 1834,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2012
      },
      {
        "Deaths": 3105,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2012
      },
      {
        "Deaths": 3544,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2012
      },
      {
        "Deaths": 501,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2012
      },
      {
        "Deaths": 16,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 2012
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 2012
      },
      {
        "Deaths": 21,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2012
      },
      {
        "Deaths": 22225,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2013
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 2013
      },
      {
        "Deaths": 1120,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2013
      },
      {
        "Deaths": 529,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2013
      },
      {
        "Deaths": 1821,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2013
      },
      {
        "Deaths": 8603,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2013
      },
      {
        "Deaths": 9836,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2013
      },
      {
        "Deaths": 235,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2013
      },
      {
        "Deaths": 46,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 2013
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 2013
      },
      {
        "Deaths": 35,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2013
      },
      {
        "Deaths": 20882,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2014
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 2014
      },
      {
        "Deaths": 774,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2014
      },
      {
        "Deaths": 12911,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2014
      },
      {
        "Deaths": 1168,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2014
      },
      {
        "Deaths": 1424,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2014
      },
      {
        "Deaths": 3532,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2014
      },
      {
        "Deaths": 943,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2014
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 2014
      },
      {
        "Deaths": 102,
        "Entity": "Volcanic activity",
        "Missing": "0",
        "Year": 2014
      },
      {
        "Deaths": 16,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2014
      },
      {
        "Deaths": 23893,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2015
      },
      {
        "Deaths": 35,
        "Entity": "Drought",
        "Missing": "0",
        "Year": 2015
      },
      {
        "Deaths": 9550,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2015
      },
      {
        "Deaths": 1032,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2015
      },
      {
        "Deaths": 7425,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2015
      },
      {
        "Deaths": 1270,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2015
      },
      {
        "Deaths": 3495,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2015
      },
      {
        "Deaths": 1006,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2015
      },
      {
        "Deaths": 13,
        "Entity": "Mass movement (dry)",
        "Missing": "0",
        "Year": 2015
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 2015
      },
      {
        "Deaths": 67,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2015
      },
      {
        "Deaths": 10201,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2016
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 2016
      },
      {
        "Deaths": 1311,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2016
      },
      {
        "Deaths": 1520,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2016
      },
      {
        "Deaths": 490,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2016
      },
      {
        "Deaths": 1760,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2016
      },
      {
        "Deaths": 4720,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2016
      },
      {
        "Deaths": 361,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2016
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 2016
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 2016
      },
      {
        "Deaths": 39,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2016
      },
      {
        "Deaths": 2087,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2017
      },
      {
        "Deaths": 0,
        "Entity": "Drought",
        "Missing": "1",
        "Year": 2017
      },
      {
        "Deaths": 49,
        "Entity": "Earthquake",
        "Missing": "0",
        "Year": 2017
      },
      {
        "Deaths": 386,
        "Entity": "Epidemic",
        "Missing": "0",
        "Year": 2017
      },
      {
        "Deaths": 130,
        "Entity": "Extreme temperature",
        "Missing": "0",
        "Year": 2017
      },
      {
        "Deaths": 394,
        "Entity": "Extreme weather",
        "Missing": "0",
        "Year": 2017
      },
      {
        "Deaths": 648,
        "Entity": "Flood",
        "Missing": "0",
        "Year": 2017
      },
      {
        "Deaths": 405,
        "Entity": "Landslide",
        "Missing": "0",
        "Year": 2017
      },
      {
        "Deaths": 0,
        "Entity": "Mass movement (dry)",
        "Missing": "1",
        "Year": 2017
      },
      {
        "Deaths": 0,
        "Entity": "Volcanic activity",
        "Missing": "1",
        "Year": 2017
      },
      {
        "Deaths": 75,
        "Entity": "Wildfire",
        "Missing": "0",
        "Year": 2017
      }
    ]
  },
  "layer": [
    {
      "data": {
        "name": "data-bc4a679881a2f6c12b6dbb818d1a0f16"
      },
      "encoding": {
        "color": {
          "field": "Entity",
          "type": "nominal"
        },
        "x": {
          "aggregate": "sum",
          "field": "Missing",
          "stack": "zero",
          "type": "quantitative"
        },
        "y": {
          "field": "Entity",
          "type": "nominal"
        }
      },
      "mark": "bar"
    },
    {
      "data": {
        "name": "data-bc4a679881a2f6c12b6dbb818d1a0f16"
      },
      "encoding": {
        "text": {
          "aggregate": "sum",
          "field": "Missing",
          "type": "quantitative"
        },
        "x": {
          "aggregate": "sum",
          "field": "Missing",
          "stack": "zero",
          "type": "quantitative"
        },
        "y": {
          "field": "Entity",
          "type": "nominal"
        }
      },
      "mark": {
        "color": "black",
        "dx": 8,
        "dy": 0,
        "type": "text"
      }
    }
  ]
};
  vegaEmbed('#vis17', yourVlSpec);
</script>


{% include custom/series_vega-in-r_next.html %}
