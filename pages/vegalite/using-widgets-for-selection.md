---
title: Using widgets for selection
keywords: vegalite
sidebar: vegalite_sidebar
permalink: vegalite-using-widgets-for-selection.html
folder: vega-lite
series: vegalite-series
weight: 14
---

Based on what we've seen so far, we can create selections by dragging across or clicking on datapoints. In other words: our selections are at the level of specific datapoints. Often, however, we'll want to select datapoints based on one or more of their features. For the cars dataset, we might for example want to select all cars that are made in the US.

### Using widgets for selection
In addition to dragging and/or clicking, we can use HTML widgets to create selections. For this we'll bind an HTML input element to a data field. In the example below, we use a selection that looks like this:

```text
"my_selection": {
  "type": "single",
  "fields": <array_of_fields>,
  "bind": {"input": <type_of_html_element>, "options": <array_of_options>}
}
```

The `fields` key points to the feature in the data that should be filtered. This should be an array, so e.g. `["Origin"]` instead of `"Origin"`. The `bind` key points to the HTML element itself. The information that we need is the type of input element (for all types, see below), and - for a `"select"` element in this case - the options that should be in the dropdown box.

```json
{
  "title": "Making selections",
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
  },
  "selection": {
    "my_selection": {
      "type": "single",
      "fields": ["Origin"],
      "bind": {"input": "select", "options": [null, "Europe", "Japan", "USA"]}
    }
  },
  "mark": "circle",
  "encoding": {
    "x": {"field": "Acceleration", "type": "quantitative"},
    "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
    "color": {
      "condition": {
        "selection": "my_selection",
        "value": "red"
      },
      "value": "lightgrey"
    }
  }
}
```

The `null` as first option in the dropdown box makes sure that all points are selected if no option is selected.

<div id="vis8"></div>
<script type="text/javascript">
  var yourVlSpec = {
    "title": "Making selections",
    "data": {
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/cars.json"
    },
    "selection": {
      "my_selection": {
        "type": "single",
        "fields": ["Origin"],
        "bind": {"input": "select", "options": [null, "Europe", "Japan", "USA"]}
      }
    },
    "mark": "circle",
    "encoding": {
      "x": {"field": "Acceleration", "type": "quantitative"},
      "y": {"field": "Miles_per_Gallon", "type": "quantitative"},
      "color": {
        "condition": {
          "selection": "my_selection",
          "value": "red"
        },
        "value": "lightgrey"
      }
    }
  };
  vegaEmbed('#vis8', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vegalite-inputbinding.png" width="50%" />
-->

This code is exactly the same as above in the example for "Selecting datapoints"; only the `selection` section is replaced from

```json
"selection": {
  "my_selection": {"type": "interval", "empty": "none"}
},
```

to

```json
"selection": {
  "my_selection": {
    "type": "single",
    "fields": ["Origin"],
    "bind": {"input": "select", "options": [null, "Europe", "Japan", "USA"]}
  }
},
```

We can also combine different selections, by using the `and` key and providing an array of selectors.

```json
"color": {
  "condition": {
    "selection": {"and": ["my_first_selection","my_second_selection"]},
    "value": "red"
  },
  "value": "lightgrey"
}
```

{:.exercise}
**Exercise** - Create a plot like the one above, but with 2 dropdown boxes: one for number of cylinders, and one for origin. All points should be lightgrey, _unless_ they comply to both criteria.

{:.exercise}
**Exercise** - Create a plot like the one above, but with 2 dropdown boxes: one for number of cylinders, and one for origin. All points should be lightgrey, _unless_ they comply to _either one_ of the criteria.

Another way of combining two filters, is to put them both in the `bind` section:

```json
"selection": {
  "my_selection": {
    "type": "single",
    "fields": ["Origin","Cylinders"],
    "bind": {
      "Origin": {"input": "select", "options": [null, "Europe", "Japan", "USA"]},
      "Cylinders": {"input": "select", "options": [null, 2,3,4,5,6,7,8]}
  }
}
```

### Types of widgets
There is more than just the dropdown widget. Here are the options:

* `select`: dropdown widget (only one selection possible)
* `range`: slider
  * e.g. `"Cylinders": {"input": "range", "min": 3, "max": 8, "step": 1}`
* `text`
  * e.g. `"Origin": {"input": "text"}`
* `checkbox`: a single checkbox
  * e.g. `"electric": {"input": "checkbox"}`
* `radio`: radio buttons
  * e.g. `"Origin": {"input": "radio", "options": ["Europe", "Japan", "USA"]}`

The different types of widgets require different arguments, so check the documentation.

{:.exercise}
**Exercise** - Alter the last plot so that you use radio buttons for the origin, and a slider for number of cylinders.

{% include custom/series_vegalite_next.html %}
