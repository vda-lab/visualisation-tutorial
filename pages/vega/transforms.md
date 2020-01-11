---
title: Transforms
keywords: vega
sidebar: vega_sidebar
permalink: vega-transforms.html
folder: vega
series: vega-series
weight: 10
---

In the vega-lite tutorial, we saw how we can use transforms to preprocess the data before it gets plotted. We can filter the data, aggregate it, compute a formula, sample, etc. For a full list of possible transformations, see the `transform` documentation at [https://vega.github.io/vega/docs/transforms/](https://vega.github.io/vega/docs/transforms/).

As we can define different datasets in vega (which is not possible in vega-lite), we can independently define different subsets of the data, or aggregations.

Creating a subset of the data just for the European cars, we can do the following:

```json
"data": [
  {
    "name": "cars",
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  {
    "name": "euro-cars",
    "source": "cars",
    "transform": [
      {"type": "filter", "expr": "datum.Origin == 'Europe'"}
    ]
  }
]
```

This creates the `cars` dataset as we had before, but also a subset of European cars.

{:.exercise}
**Exercise** - How would we now use this filtered dataset for the marks? Make an acceleration versus mpg plot for only the european cars.

We can do the same for aggregation to create a histogram. Whereas the original data is not available anymore in vega-lite, it can still be in vega.

```json
...
"data": [
  {
    "name": "cars",
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  {
    "name": "binned",
    "source": "cars",
    "transform": [
      {"type": "bin", "field": "Acceleration", "extent": [0,25]}
    ]
  },
  {
    "name": "aggregated",
    "source": "binned",
    "transform": [
      {"type": "aggregate",
        "key": "bin0", "groupby": ["bin0", "bin1"],
        "fields": ["bin0"], "ops": ["count"], "as": ["count"]}
    ]
  }
],
...
```

There are now three different datasets available: `cars`, `binned` and `aggregated`. We can have each separate like this, or - as we don't expect to ever use the `binned` dataset by itself, merge `binned` and `aggregated` like we had to do in vega-lite anyway:

```json
...
"data": [
  {
    "name": "cars",
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  {
    "name": "aggregated",
    "source": "cars",
    "transform": [
      {"type": "aggregate",
        "key": "bin0", "groupby": ["bin0", "bin1"],
        "fields": ["bin0"], "ops": ["count"], "as": ["count"]},
      {"type": "bin", "field": "Acceleration", "extent": [0,25]}
    ]
  }
],
...
```

Important tip: when using the vega editor at [https://vega.github.io/editor](https://vega.github.io/editor), have a look at the data viewer in the lower-right corner: it shows you what each of the datasets looks like.

The original dataset:

<img src="{{ site.baseurl }}/assets/vega-dataviewer-cars.png"/>

The `binned` dataset (note the two additional columns at the end):

<img src="{{ site.baseurl }}/assets/vega-dataviewer-binned.png"/>

The `aggregated` dataset:

<img src="{{ site.baseurl }}/assets/vega-dataviewer-aggregated.png" width="30%"/>

{% include custom/series_vega_next.html %}
