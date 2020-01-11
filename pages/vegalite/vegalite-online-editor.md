---
title: Vega-Lite online editor
keywords: vegalite
sidebar: vegalite_sidebar
permalink: vegalite-vegalite-online-editor.html
folder: vega-lite
series: vegalite-series
weight: 2
---
![vegalite-online-editor]({{ site.baseurl }}/assets/vegalite-online-editor.png)

We'll use the vega-lite online editor at [https://vega.github.io/editor/](https://vega.github.io/editor/). From the pull-down menu in the top-left, select "Vega-Lite" if it is not selected. From "Examples", select "Simple Bar Chart" (make sure that you are in the "Vega-Lite" tab).

![vegalite-barchart-example]({{ site.baseurl }}/assets/vegalite-barchart-example.png)

You'll see an editor screen on the left with what is called the vega-lite _specification_, the output on the top right, and a debugging area in the bottom right. We'll come back to debugging later. Whenever you change the specification in the editor, the output is automatically updated.

{:.exercise}
**Exercise** - Add an additional bar to the plot with a value of 100.

{:.exercise}
**Exercise** - Change the mark type from `bar` to `point`.

{:.exercise}
**Exercise** - Looking at the vega-lite documentation at [https://vega.github.io/vega-lite/docs/](https://vega.github.io/vega-lite/docs/), check what other types of mark are available. See which of these actually work with this data.

{:.exercise}
**Exercise** - How would you make this an horizontal chart?
<!--
Flip x and y
-->

The `encoding` section specifies what is called the "visual encoding": it links fields in each data object (in this case: fields `a` and `b`) to visual channels (in this case: `x` and `y`). The field names should correspond to a field in the dataset, and the keys (`x` and `y`) depend on the type of mark you choose. Again: the [documentation](https://vega.github.io/vega-lite/docs/field.html) is very helpful.

{:.exercise}
**Exercise** - Add a new field to the datapoints in the dataset with some integer value, called `new_field`. Next, change the plot so that you have a scatterplot with this new field on the y-axis and the field `b` on the x-axis.
<!--
{
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "description": "A simple bar chart with embedded data.",
  "data": {
    "values": [
      {"a": "A", "b": 28, "new_field": 15},
      {"a": "B", "b": 55, "new_field": 14},
      {"a": "C", "b": 43, "new_field": 53},
      {"a": "D", "b": 91, "new_field": 12},
      {"a": "E", "b": 81, "new_field": 2},
      {"a": "F", "b": 53, "new_field": 62},
      {"a": "G", "b": 19, "new_field": 54},
      {"a": "H", "b": 87, "new_field": 84},
      {"a": "I", "b": 52, "new_field": 47},
      {"a": "J", "b": 100, "new_field": 33}
    ]
  },
  "mark": "circle",
  "encoding": {
    "x": {"field": "b", "type": "quantitative"},
    "y": {"field": "new_field", "type": "quantitative"}
  }
}
-->

{% include custom/series_vegalite_next.html %}
