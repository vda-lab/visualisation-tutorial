---
title: "Data Visualisation in Data Science"
keywords: homepage
permalink: index.html
---
![]({{ site.baseurl }}/assets/stad_airquality.jpeg)

Welcome to this set of tutorials for data visualisation. These were created to serve as teaching material for the EBI workshop [Data Visualisation for Biology: A Practical Workshop on Design, Techniques and Tools](https://www.ebi.ac.uk/training/events/2020/data-visualisation-biology-practical-workshop-design-techniques-and-tools-1) as well as the course material for the Data Visualisation for Data Science courses at [UHasselt](https://www.uhasselt.be/studiegids?n=4&a=2019&i=4142) and [KU Leuven](https://onderwijsaanbod.kuleuven.be/syllabi/e/G0R72AE.htm#activetab=doelstellingen_idm480336).

The contents of these tutorials is licensed as CC-BY: feel free to copy/remix/tweak/... it, but please credit your source.

![CC-BY]({{ site.baseurl }}/assets/ccby.png)

In these tutorial, we will work in different phases, looking at vega-lite, vega, and Holoviz. We'll start with vega-lite and vega in the [online editor](https://vega.github.io/editor/) that they provide, and move on to using holoviz at a later stage.

This tutorial is based on material provided on the vega-lite, vega and holoviz websites, as well as teaching material collected by Ryo Sakai.

## Preamble
### What are vega-lite and vega?
You might have heard of [D3](http://d3js.org) as a library to create interactive data visualisations. Indeed, this library is considered the standard in the field. Unfortunately, it does have quite a steep learning curve which makes it not ideal if you have to learn it in 2-3 days without a background in javascript programming. In this course, we'll use vega and vega-lite instead. Both are so-called _declarative_ languages, where you tell the computer _what_ you need, not _how_ to do it. Vega and vega-lite are expressed in _JSON_ ("javascript object notation").

This image by [Eric Marty](https://blog.ericmarty.com/the-d3-/-vega-stack) provides a good overview how the different parts are related:

<img src="{{ site.baseurl }}/assets/d3-vega-vegalite-stack.png" />

To give you an idea, here's a small vega-lite script that shows a barchart.

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "data": {
    "values": [
      {"a": "A", "b": 28}, {"a": "B", "b": 55}, {"a": "C", "b": 43}
    ]
  },
  "mark": "bar",
  "encoding": {
    "x": {"field": "b", "type": "quantitative"},
    "y": {"field": "a", "type": "ordinal"}
  }
}
```

The resulting barchart:

<img src="{{ site.baseurl }}/assets/vegalite-barchart.png" width="300px"/>

### JSON
Let's first have a look at the JSON format:

- strings are put between double quotes `"`
- numbers are _not_ put between quotes
- lists (aka arrays) are put between square brackets `[]`
- objects (aka hashes, aka dictionaries, aka key-value pairs) are put between curly brackets `{}`, and key and value are separated with a colon `:`

Also, these objects can be nested. In the example above, the whole thing is a single JSON object, consisting of key-value pairs (keys being `"$schema"`, `"data"`, `"mark"` and `"encoding"`). The `"data"` key itself holds an object `{ "values": [ ... ]}`. The `"values"` key in its place is an array of objects again.

Different elements in a JSON object or array have to be separated by a comma `,`.

## The actual tutorials

* [Vega-Lite]({{ site.baseurl }}/vegalite_landing_page.html)
* [Vega]({{ site.baseurl }}/vega_landing_page.html)
* [Holoviz]()
