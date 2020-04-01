---
title: Field Transform
keywords: vega-in-r
sidebar: vega-in-r_sidebar
permalink: /vega-in-r-field-transform.html
folder: vega-in-r
series: vega-in-r-series
weight: 5
---

Since we are wokring in R, we can modify the data outside the plot specification and then use the modified dataset inside the plot encoding.
However, using the altair package, calculations inside the plot specification can be sometimes easier. In this section, we are discussing field trasforms that can be done inside encoding.
As we have seen from the beginning of this tutorial, the `encoding` determines the mapping between the channels and the data. We have already used encoding channels such as position channels `x` and `y` and mark property channels, for instance, `color` and `opacity`.
We only need to add `bin = TRUE` in the `x` position channel of a quantitative field to use the binned version of the field in the plot.
Below, there is the code to produce a barchart of the sum of deaths versus the binned years.

```R
data_source_subset = subset(data_source, data_source$Entity == "All natural disasters") 

chart_disasters = alt$Chart(data_source_subset)$
  mark_bar()$
  encode(
    x = alt$X("Year:Q", bin = TRUE),
    y = 'sum(Deaths):Q',
    tooltip = 'sum(Deaths):Q'
  )
```

<div id="vis8"></div>
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
    "tooltip": {
      "aggregate": "sum",
      "field": "Deaths",
      "type": "quantitative"
    },
    "x": {
      "bin": true,
      "field": "Year",
      "type": "quantitative"
    },
    "y": {
      "aggregate": "sum",
      "field": "Deaths",
      "type": "quantitative"
    }
  },
  "mark": "bar",
  "transform": [
    {
      "filter": {
        "equal": "All natural disasters",
        "field": "Entity"
      }
    }
  ]
};
  vegaEmbed('#vis8', yourVlSpec);
</script>

<br/>

Mind the difference in the syntax here. We used the long form `x = alt$X()`, we have seen in the simple barchart section, so that we can specify the binning inside encoding. Other adjustments can be related to scale or axis.  

<br/>

{:.exercise}
**Exercise** - Check the documentation of the binning parameters [https://altair-viz.github.io/user_guide/generated/core/altair.BinParams.html](https://altair-viz.github.io/user_guide/generated/core/altair.BinParams.html) and increase the value of the maximum number of bins.

<div id="vis9"></div>
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
    "tooltip": {
      "aggregate": "sum",
      "field": "Deaths",
      "type": "quantitative"
    },
    "x": {
      "bin": {
        "maxbins": 50
      },
      "field": "Year",
      "type": "quantitative"
    },
    "y": {
      "aggregate": "sum",
      "field": "Deaths",
      "type": "quantitative"
    }
  },
  "mark": "bar",
  "transform": [
    {
      "filter": {
        "equal": "All natural disasters",
        "field": "Entity"
      }
    }
  ]
};
  vegaEmbed('#vis9', yourVlSpec);
</script>

<br/>

{:.exercise}
**Exercise** - Using `data_source_subset = subset(data_source, data_source$Entity != "All natural disasters")` make a heatmap that shows the count of disasters per year, like the one below.

<br/>

<div id="vis10"></div>
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
      "aggregate": "count",
      "field": "Entity",
      "legend": {
        "title": "Count Disasters"
      },
      "type": "quantitative"
    },
    "tooltip": [
      {
        "field": "Year",
        "type": "ordinal"
      },
      {
        "aggregate": "count",
        "field": "Entity",
        "type": "quantitative"
      }
    ],
    "x": {
      "field": "Year",
      "type": "ordinal"
    }
  },
  "height": 100,
  "mark": "rect",
  "selection": {
    "selector028": {
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
  "width": 800
};
  vegaEmbed('#vis10', yourVlSpec);
</script>

<br/>

Another filed transformation is the one that scales the original field domain to the custom range we specify. 
For instance, we can transform a quantitative field using the log scale, as we can see below.


```R
chart_disasters = alt$Chart("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv")$
  mark_bar()$
  encode(
    x = 'Entity:N',
    y = alt$Y('sum(Deaths):Q', scale=alt$Scale(type='log'))
  )$
  properties(
    height = 300,
    width = 600
  ) 
```

<div id="vis11"></div>
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
      "field": "Entity",
      "type": "nominal"
    },
    "y": {
      "aggregate": "sum",
      "field": "Deaths",
      "scale": {
        "type": "log"
      },
      "type": "quantitative"
    }
  },
  "height": 300,
  "mark": "bar",
  "width": 600
};
  vegaEmbed('#vis11', yourVlSpec);
</script>

<br/>

Fortunately, not in all years from 1900 to 2017 all types of registered disasters occured. Did you notice that in 1904 there is no natural disaster registered? 
Let's enrich the dataset in R with a variable for missing values based on the year.

```R
data_source = read.csv(url("https://raw.githubusercontent.com/vega/vega-datasets/master/data/disasters.csv")) # original data
Year = seq(1900, 2017, 1) # create year vector 
Entity = sort(rep(unique(data_source$Entity), 118)) # create entity vector
data_mod = cbind.data.frame(Year, Entity) # create dataframe with complete set of year and entity
data_source_modified = merge(data_source, data_mod, by = c("Year", "Entity"), all = T) # merge df with original data
data_source_modified[is.na(data_source_modified$Deaths),"Deaths"] = 0 # replace NA with zero
data_source_modified$Missing = NULL # create new variable
data_source_modified[data_source_modified$Deaths == 0,"Missing"] = "1" # the value for missing
data_source_modified[data_source_modified$Deaths != 0,"Missing"] = "0" # the value for non-missing
str(data_source_modified) # look at the new data structure
rm(Year, Entity, data_mod) # remove objects that are not needed
```

Now we can plot the full time series, and specify a custom color scale for the presence of absence of the year in the data.
So, the domain of the data is `0` for Non-Missing, `1` for Missing and the custom range is the two colors of our preference, here black and red.

```R
domain_var = c("0", "1")
range_color = c('black', 'red')
range_size = c(50, 150)

data_source_subset = subset(data_source_modified, data_source_modified$Entity == "All natural disasters")

chart_disasters = alt$Chart(data_source_subset)$
  mark_circle(
    opacity = 0.8
  )$
  encode(
    x = 'Year:O',
    y = 'Deaths:Q',
    color = alt$Color('Missing', scale = alt$Scale(domain = domain_var, range = range_color)),
    size = alt$Size('Missing', scale = alt$Scale(domain = domain_var, range = range_size)),
    tooltip = c("Year", "Deaths")
  )$
  properties(
    height = 300,
    width = 600
  )$
  interactive()
```


<div id="vis12"></div>
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
    "name": "data-7d530dfc1e453b68646c99727cfcb055"
  },
  "datasets": {
    "data-7d530dfc1e453b68646c99727cfcb055": [
      {
        "Deaths": 1267360,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1900
      },
      {
        "Deaths": 200018,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1901
      },
      {
        "Deaths": 46037,
        "Entity": "All natural disasters",
        "Missing": "0",
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
        "Entity": "All natural disasters",
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
        "Deaths": 42970,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1906
      },
      {
        "Deaths": 1325641,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1907
      },
      {
        "Deaths": 75033,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1908
      },
      {
        "Deaths": 1511524,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1909
      },
      {
        "Deaths": 148233,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1910
      },
      {
        "Deaths": 102408,
        "Entity": "All natural disasters",
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
        "Deaths": 882,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1913
      },
      {
        "Deaths": 289,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1914
      },
      {
        "Deaths": 32167,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1915
      },
      {
        "Deaths": 300,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1916
      },
      {
        "Deaths": 2523507,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1917
      },
      {
        "Deaths": 461113,
        "Entity": "All natural disasters",
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
        "Deaths": 3204224,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1920
      },
      {
        "Deaths": 1200000,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1921
      },
      {
        "Deaths": 101243,
        "Entity": "All natural disasters",
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
        "Deaths": 303009,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1924
      },
      {
        "Deaths": 5832,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1925
      },
      {
        "Deaths": 427852,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1926
      },
      {
        "Deaths": 215160,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1927
      },
      {
        "Deaths": 3004895,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1928
      },
      {
        "Deaths": 8377,
        "Entity": "All natural disasters",
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
        "Deaths": 3706227,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1931
      },
      {
        "Deaths": 73296,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1932
      },
      {
        "Deaths": 34296,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1933
      },
      {
        "Deaths": 21087,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1934
      },
      {
        "Deaths": 272817,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1935
      },
      {
        "Deaths": 5301,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1936
      },
      {
        "Deaths": 12025,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1937
      },
      {
        "Deaths": 2225,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1938
      },
      {
        "Deaths": 563178,
        "Entity": "All natural disasters",
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
        "Deaths": 10195,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1941
      },
      {
        "Deaths": 1608235,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1942
      },
      {
        "Deaths": 1910322,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1943
      },
      {
        "Deaths": 15906,
        "Entity": "All natural disasters",
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
        "Deaths": 35490,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1946
      },
      {
        "Deaths": 17647,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1947
      },
      {
        "Deaths": 120131,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1948
      },
      {
        "Deaths": 120370,
        "Entity": "All natural disasters",
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
        "Deaths": 15042,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1951
      },
      {
        "Deaths": 8965,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1952
      },
      {
        "Deaths": 12956,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1953
      },
      {
        "Deaths": 41872,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1954
      },
      {
        "Deaths": 6026,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1955
      },
      {
        "Deaths": 7737,
        "Entity": "All natural disasters",
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
        "Deaths": 3950,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1958
      },
      {
        "Deaths": 2013242,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1959
      },
      {
        "Deaths": 39188,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1960
      },
      {
        "Deaths": 17341,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1961
      },
      {
        "Deaths": 17370,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1962
      },
      {
        "Deaths": 37746,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1963
      },
      {
        "Deaths": 12892,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1964
      },
      {
        "Deaths": 1565517,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1965
      },
      {
        "Deaths": 17181,
        "Entity": "All natural disasters",
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
        "Deaths": 21461,
        "Entity": "All natural disasters",
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
        "Deaths": 387507,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1970
      },
      {
        "Deaths": 18086,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1971
      },
      {
        "Deaths": 20045,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1972
      },
      {
        "Deaths": 110555,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1973
      },
      {
        "Deaths": 87504,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1974
      },
      {
        "Deaths": 14858,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1975
      },
      {
        "Deaths": 280469,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1976
      },
      {
        "Deaths": 22406,
        "Entity": "All natural disasters",
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
        "Deaths": 7341,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1979
      },
      {
        "Deaths": 23089,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 1980
      },
      {
        "Deaths": 119697,
        "Entity": "All natural disasters",
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
        "Deaths": 461561,
        "Entity": "All natural disasters",
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
        "Deaths": 60232,
        "Entity": "All natural disasters",
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
        "Deaths": 21533,
        "Entity": "All natural disasters",
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
        "Deaths": 12611,
        "Entity": "All natural disasters",
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
        "Deaths": 189707,
        "Entity": "All natural disasters",
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
        "Deaths": 21821,
        "Entity": "All natural disasters",
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
        "Deaths": 27166,
        "Entity": "All natural disasters",
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
        "Deaths": 30124,
        "Entity": "All natural disasters",
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
        "Deaths": 76886,
        "Entity": "All natural disasters",
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
        "Deaths": 39493,
        "Entity": "All natural disasters",
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
        "Deaths": 113558,
        "Entity": "All natural disasters",
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
        "Deaths": 93566,
        "Entity": "All natural disasters",
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
        "Deaths": 22422,
        "Entity": "All natural disasters",
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
        "Deaths": 16037,
        "Entity": "All natural disasters",
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
        "Deaths": 34143,
        "Entity": "All natural disasters",
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
        "Deaths": 22225,
        "Entity": "All natural disasters",
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
        "Deaths": 23893,
        "Entity": "All natural disasters",
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
        "Deaths": 2087,
        "Entity": "All natural disasters",
        "Missing": "0",
        "Year": 2017
      }
    ]
  },
  "encoding": {
    "color": {
      "field": "Missing",
      "scale": {
        "domain": [
          "0",
          "1"
        ],
        "range": [
          "black",
          "red"
        ]
      },
      "type": "nominal"
    },
    "size": {
      "field": "Missing",
      "scale": {
        "domain": [
          "0",
          "1"
        ],
        "range": [
          50,
          150
        ]
      },
      "type": "nominal"
    },
    "tooltip": [
      {
        "field": "Year",
        "type": "quantitative"
      },
      {
        "field": "Deaths",
        "type": "quantitative"
      }
    ],
    "x": {
      "field": "Year",
      "type": "ordinal"
    },
    "y": {
      "field": "Deaths",
      "type": "quantitative"
    }
  },
  "height": 300,
  "mark": {
    "opacity": 0.8,
    "type": "circle"
  },
  "selection": {
    "selector005": {
      "bind": "scales",
      "encodings": [
        "x",
        "y"
      ],
      "type": "interval"
    }
  },
  "width": 600
};
  vegaEmbed('#vis12', yourVlSpec);
</script>



{% include custom/series_vega-in-r_next.html %}
