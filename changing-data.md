---
title: Changing data
keywords: vega-in-r
sidebar: vega-in-r_sidebar
permalink: /vega-in-r-changing-data.html
folder: vega-in-r
series: vega-in-r-series
weight: 3
---
Let's now use a more realistic example and visualize a dataset included in the `vega_datasets` package [https://github.com/vega/vega-datasets.html](https://github.com/vega/vega-datasets.html).

We can import the vega datasets using the altair library.
```R
vega_data = altair::import_vega_data()
```

Check out the list of the available datasets:
```R
vega_data$list_datasets()
```

and select the one you want to work with. Here, we are using the dataset for [Natural Disasters from Our World in Data](https://ourworldindata.org/natural-disasters.html).
```R
data_source = vega_data$disasters()
```

Alternatively, you may load data from a local file using standard R code, or read the data from a url using:
```R
data_source = read.csv(url("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv"))
```

After importing the data, we can take a first look using standard R code:

```R
str(data_source)
summary(data_source)
head(data_source); tail(data_source)
```

```R
> str(data_source)
'data.frame':	803 obs. of  3 variables:
 $ Entity: Factor w/ 11 levels "All natural disasters",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ Year  : int  1900 1901 1902 1903 1905 1906 1907 1908 1909 1910 ...
 $ Deaths: int  1267360 200018 46037 6506 22758 42970 1325641 75033 1511524 148233 ...
> summary(data_source)
                   Entity         Year          Deaths       
 All natural disasters:117   Min.   :1900   Min.   :      1  
 Earthquake           :111   1st Qu.:1946   1st Qu.:    270  
 Extreme weather      :111   Median :1975   Median :   1893  
 Flood                : 89   Mean   :1969   Mean   :  81213  
 Landslide            : 79   3rd Qu.:1996   3rd Qu.:  10362  
 Epidemic             : 69   Max.   :2017   Max.   :3706227  
 (Other)              :227                                   
> head(data_source)
                 Entity Year  Deaths
1 All natural disasters 1900 1267360
2 All natural disasters 1901  200018
3 All natural disasters 1902   46037
4 All natural disasters 1903    6506
5 All natural disasters 1905   22758
6 All natural disasters 1906   42970
> tail(data_source)
      Entity Year Deaths
798 Wildfire 2012     21
799 Wildfire 2013     35
800 Wildfire 2014     16
801 Wildfire 2015     67
802 Wildfire 2016     39
803 Wildfire 2017     75
```

We can now make an altair R plot similar to the one at altair Python [https://altair-viz.github.io/gallery/natural_disasters.html](https://altair-viz.github.io/gallery/natural_disasters.html)
For now, we may filter the data in R and use the subset of the data to make the chart. On the data transform section we will see how to do the filtering inside the chart specification.

<br/>

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
  "width": 500
};
  vegaEmbed('#vis3', yourVlSpec);
</script>


Below is the code to make this plot.
```R
data_source_subset = subset(data_source, data_source$Entity != "All natural disasters") 

chart_disasters = alt$Chart(data_source_subset)$
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
  )$
  properties(
    height=200,
    width=500
  )
```
Here, the global properties of the circles are specified inside the mark attribute while the properties that depend on the data inside the encoding.
Using the mark type `rect` with `color` and `opacity` channels we can make a heatmap plot. 


```R
chart_disasters = alt$Chart(data_source_subset)$
  mark_rect()$
  encode(
    x = "Entity:O",
    y = "Year:O",
    color = "Entity:N",
    opacity = 'Deaths:Q'
  )$
  properties(
    height=600,
    width=200
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
  )$
  properties(
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


{% include custom/series_vega-in-r_next.html %}
