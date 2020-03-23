---
title: A case study
keywords: vega-in-r
sidebar: vega-in-r_sidebar
permalink: /vega-in-r-a-case-study.html
folder: vega-in-r
series: vega-in-r-series
weight: 3
---
Let's now use a more realistic example and visualize the natural diasters dataset [https://ourworldindata.org/natural-disasters.html](https://ourworldindata.org/natural-disasters.html). 
This dataset is included in the vega_datasets package [https://github.com/vega/vega-datasets.html] (https://github.com/vega/vega-datasets.html).

You can import the datasets using the altair library.
vega_data = altair::import_vega_data()

See the list of the available datasets
```R
vega_data$list_datasets()
```

and select the one you want to visualise.
```R
data_source = vega_data$disasters()
```

Alternatively, you may read the data from a url using:
```R
data_source = read.csv(url("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv"))
```

or load the data from a local file using standard R code.

After importing the data, we can take a first look using standard R code:

```R
str(data_source)
summary(data_source)
head(data_source); tail(data_source)
```

We can now make a plot similar to the one at [https://altair-viz.github.io/gallery/natural_disasters.html](https://altair-viz.github.io/gallery/natural_disasters.html)
For now, we may filter tha data in R and use the subset of the data to make the plot in altair R. On the data transformations section we will see how to do the filtering inside the altair specification.

<div id="vis3"></div>
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
    "size": {
      "field": "Deaths",
      "type": "quantitative"
    },
    "x": {
      "field": "Year",
      "type": "ordinal"
    },
    "y": {
      "field": "Entity",
      "type": "nominal"
    }
  },
  "height": 200,
  "mark": {
    "opacity": 0.8,
    "stroke": "black",
    "strokeWidth": 1,
    "type": "circle"
  },
  "width": 400
};
  vegaEmbed('#vis3', yourVlSpec);
</script>


Below is the code to make this plot.

```R
data_source_subset = subset(data_source, data_source$Entity != "All natural disasters") 

chart_disasters = 
  alt$Chart(data_source_subset)$
  mark_circle(
    opacity=0.8,
    stroke='black',
    strokeWidth=1
  )$
  encode(
    x = "Year:O",
    y = "Entity:N",
    color = "Entity:N",
    size = "Deaths:Q"
  )$properties(
    height=200,
    width=400
  )
```
The global properties of the circles are specified inside the mark attribute and the properties that depend on the data inside the encoding.
Using the mark type `rect` with `color` and `opacity` channels we can make a heatmap plot. 


```R
chart_disasters = 
  alt$Chart(data_source_subset)$
  mark_circle(
    opacity=0.8,
    stroke='black',
    strokeWidth=1
  )$
  encode(
    x = "Year:O",
    y = "Entity:N",
    color = "Entity:N",
    size = "Deaths:Q"
  )$properties(
    height=200,
    width=400
  )
```


<div id="vis4"></div>
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
  vegaEmbed('#vis4', yourVlSpec);
</script>

Next, using the code below, we can make a time series plot of deaths from all natural disasters from 1900 until 2017.

```R
data_source_subset = subset(data_source, data_source$Entity == "All natural disasters") 

chart_disasters = alt$Chart(data_source_subset)$
  mark_line()$
  encode(
    x='Year:Q',
    y='Deaths:Q',
    tooltip = c("Year", "Deaths")
  )$properties(
    height=300,
    width=600
)
```

<div id="vis5"></div>
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
  vegaEmbed('#vis5', yourVlSpec);
</script>


{:.exercise}
**Exercise** - Use the `color` channel to make a time series plot per Entity.

{:.exercise}
**Exercise** - Change the field types. What is the result?

{:.exercise}
**Exercise** - Make a barchart for total deaths per Entity. Hint: You may do the calculation in R or try a calculation inside encoding.


{% include custom/series_vega-in-r_next.html %}
