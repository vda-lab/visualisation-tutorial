---
title: Further exercises
keywords: vegalite
sidebar: vegalite_sidebar
permalink: further-exercises.html
folder: vega-lite
---
For the exercises below, we will use the New York City citibike data available from [https://www.citibikenyc.com/system-data](https://www.citibikenyc.com/system-data). Some great [visuals by Juan Francisco Saldarriaga](https://juanfrans.com/projects/citibikeRebalancing.html) can inspire you.

<img src="{{ site.baseurl }}/assets/citibike_linegraph.png" />

We made a (small) part of the data available [here](https://raw.githubusercontent.com/vda-lab/vda-lab.github.io/master/assets/station_366.json). It concerns trip data from November 2011, where the trip started or ended in station nr 336. The fields in each record (with example data) look like this:

{% highlight json %}
{
  "tripduration": 1217,
  "starttime": "2019-11-01 06:03:28.5390",
  "stoptime": "2019-11-01 06:23:45.9810",
  "startstation_id": 3236,
  "startstation_name": "W 42 St & Dyer Ave",
  "startstation_latitude": 40.75898481399634,
  "startstation_longitude": -73.99379968643188,
  "endstation_id": 336,
  "endstation_name": "Sullivan St & Washington Sq",
  "endstation_latitude": 40.73047747,
  "endstation_longitude": -73.99906065,
  "bikeid": 41025,
  "usertype": "Subscriber",
  "birthyear": 1964,
  "gender": 1
}
{% endhighlight json %}

{:.exercise}
**Exercise**: Make a plot showing how the trip duration is related to the hour of the day. You could colour by usertype. You'll see that your plot will be compressed because of some very long durations, so only use the trips that have a duration of less than 5,000.

<img src="{{ site.baseurl }}/assets/vegalite-citibike-durationbyhour.png" />

<!--
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "width": 600,
  "data": {
    "url": "https://raw.githubusercontent.com/vda-lab/vda-lab.github.io/master/assets/endstation_336.json"
  },
  "transform": [
    {
      "filter": {"field": "tripduration", "lte": "5000"}
    },
    {"calculate": "hours(datum.starttime)", "as": "hour"}
  ],
  "mark": "circle",
  "encoding": {
    "x": {"field": "hour", "type": "quantitative"},
    "y": {"field": "tripduration", "type": "quantitative"},
    "color": {"field": "usertype"}
  }
}
-->

{:.exercise}
**Exercise**: Make a plot with the relative positions of the start stations vis-a-vis the end station, when that end station is 336. Show the end station itself as well. Your plot could look like this:

<img src="{{site.baseurl}}/assets/vegalite-citibike-relativepositions1.png" />

<!--
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "description": "A simple bar chart with embedded data.",
  "width": 600,
  "height": 600,
  "data": {
    "url": "https://raw.githubusercontent.com/vda-lab/vda-lab.github.io/master/assets/endstation_336.json"
  },
  "transform": [
    {
      "filter": {"field": "tripduration", "lte": "5000"}
    },
    {"calculate": "hours(datum.starttime)", "as": "hour"}
  ],
  "layer": [
    {
      "mark": "circle",
      "encoding": {
        "x": {
          "field": "startstation_longitude",
          "type": "quantitative",
          "scale": {"type": "linear", "domain": [-74.03,-73.925], "range": [0, 600]}},
        "y": {
          "field": "startstation_latitude",
          "type": "quantitative",
          "scale": {"type": "linear", "domain": [40.65,40.82], "range": [0, 600]}},
        "opacity": {"value": 0.3}
      }
    },
    {
      "mark": "circle",
      "encoding": {
        "x": {
          "field": "endstation_longitude",
          "type": "quantitative",
          "scale": {"type": "linear", "domain": [-74.04,-73.9], "range": [0, 600]}},
        "y": {
          "field": "endstation_latitude",
          "type": "quantitative",
          "scale": {"type": "linear", "domain": [40.65,40.82], "range": [0, 600]}},
        "color": {"value": "red"},
        "opacity": {"value": 0.01},
        "size": {"value": 250}
      }
    }
  ]
}
-->

{:.exercise}
**Exercise**: Same as the one above, but scale the points based on the number of bikes picked up there. You plot should look like this:

<img src="{{ site.baseurl }}/assets/vegalite-citibike-scaled.png" />

<!--
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "title": "Relative locations and importance of citibike pickup stations for dropoff station 336",
  "width": 600,
  "height": 600,
  "data": {
    "url": "https://raw.githubusercontent.com/vda-lab/vda-lab.github.io/master/assets/endstation_336.json"
  },
  "layer": [
    {
      "mark": "circle",
      "encoding": {
        "x": {
          "title": "longitude",
          "field": "startstation_longitude",
          "type": "quantitative",
          "scale": {"type": "linear", "domain": [-74.03,-73.925], "range": [0, 600]}},
        "y": {
          "title": "latitude",
          "field": "startstation_latitude",
          "type": "quantitative",
          "scale": {"type": "linear", "domain": [40.65,40.82], "range": [0, 600]}},
        "opacity": {"value": 0.5},
        "size": {"aggregate": "count", "field": "startstation_id", "type": "quantitative"}
      }
    },
    {
      "mark": "circle",
      "encoding": {
        "x": {
          "field": "endstation_longitude",
          "type": "quantitative",
          "scale": {"type": "linear", "domain": [-74.04,-73.9], "range": [0, 600]}},
        "y": {
          "field": "endstation_latitude",
          "type": "quantitative",
          "scale": {"type": "linear", "domain": [40.65,40.82], "range": [0, 600]}},
        "color": {"value": "red"},
        "opacity": {"value": 0.01},
        "size": {"value": 250}
      }
    }
  ]
}
-->

{:.exercise}
**Exercise**: Same as the one above, but facetted by hour.

<img src="{{ site.baseurl }}/assets/vegalite-citibike-facetted.png" />

<!--
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "title": "Relative locations and importance of citibike pickup stations for dropoff station 336",
  "width": 100,
  "height": 100,
  "data": {
    "url": "https://raw.githubusercontent.com/vda-lab/vda-lab.github.io/master/assets/endstation_336.json"
  },
  "transform": [
    {
      "filter": {"field": "tripduration", "lte": "5000"}
    },
    {"calculate": "hours(datum.starttime)", "as": "hour"}
  ],
  "mark": "circle",
  "encoding": {
    "facet": {
      "field": "hour",
      "type": "quantitative",
      "columns": 6
    },
    "x": {
      "title": "longitude",
      "field": "startstation_longitude",
      "type": "quantitative",
      "scale": {"type": "linear", "domain": [-74.03,-73.925]}},
    "y": {
      "title": "latitude",
      "field": "startstation_latitude",
      "type": "quantitative",
      "scale": {"type": "linear", "domain": [40.65,40.82]}},
    "opacity": {"value": 0.5},
    "size": {"aggregate": "count", "field": "startstation_id", "type": "quantitative"}
  }    
}
-->

{:.exercise}
**Exercise** - What other interesting plots could you make?
