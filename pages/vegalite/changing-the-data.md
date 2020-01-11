---
title: Changing the data
keywords: vegalite
sidebar: vegalite_sidebar
permalink: vegalite-changing-the-data.html
folder: vega-lite
---
If your dataset is a bit bigger than what you see here, it'll become cumbersome to type this into the specification. It's often better to load your data from an external source. Looking at the [documentation](https://vega.github.io/vega-lite/docs/data.html) we see that data can be inline, or loaded from a URL. There is also something called "Named data sources", but we won't look into that.

What we've done above is provide the data inline. In that case, you need the `values` key, e.g.

```json
"data": {
  "values": [
    {"a": "A", "b": 28},
    {"a": "B", "b": 55}
  ]
}
```

When loading external data, we'll need the `url` key instead:

```json
"data": {
  "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
}
```

This cars dataset is one of the standard datasets used for learning data visualisation. The json file at the URL looks like this:

```json
[
   {
      "Name":"chevrolet chevelle malibu",
      "Miles_per_Gallon":18,
      "Cylinders":8,
      "Displacement":307,
      "Horsepower":130,
      "Weight_in_lbs":3504,
      "Acceleration":12,
      "Year":"1970-01-01",
      "Origin":"USA"
   },
   {
      "Name":"buick skylark 320",
      "Miles_per_Gallon":15,
      "Cylinders":8,
      "Displacement":350,
      ...}
]
```

So it is an _array_ (`[]`) of _objects_ (`{}`) where each object is a car for which we have a name, miles per gallon, cylinders, etc.

{:.exercise}
**Exercise 5**: Alter the specification in the vega-lite editor to recreate this image:

<img src="{{ site.baseurl }}/assets/vegalite-cars-accelerationbympg.png" width="30%" />
