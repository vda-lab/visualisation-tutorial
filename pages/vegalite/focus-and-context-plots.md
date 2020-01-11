---
title: Focus and context plots
keywords: vegalite
sidebar: vegalite_sidebar
permalink: focus-and-context-plots.html
folder: vega-lite
---
Knowing how we can select/brush part of a dataset, and that we can bind these selections to a scale, we can make focus/context plots.

To do this, we define a `selection` in the _source_ plot (i.e. in the one in which we will do the selecting). This selection is then used to change the domain of the scale in the _target_ plot.

The example below shows this on the S&P500 data. Try selecting a range in the bottom plot.

<div id="vis6"></div>
<script type="text/javascript">
  var yourVlSpec = { "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
    "data": {
      "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/sp500.csv"
    },
    "vconcat": [{
      "width": 480,
      "mark": "area",
      "encoding": {
        "x": {
          "field": "date",
          "type": "temporal",
          "scale": {"domain": {"selection": "brush"}},
          "axis": {"title": ""}
        },
        "y": {"field": "price", "type": "quantitative"}
      }
    }, {
      "width": 480,
      "height": 60,
      "mark": "area",
      "selection": {
        "brush": {"type": "interval", "encodings": ["x"]}
      },
      "encoding": {
        "x": {
          "field": "date",
          "type": "temporal"
        },
        "y": {
          "field": "price",
          "type": "quantitative",
          "axis": {"grid": false}
        }
      }
    }]
  };
  vegaEmbed('#vis6', yourVlSpec);
</script>

<!--
<img src="{{ site.baseurl }}/assets/vega-focuscontext.png" width="50%"/>
-->

{% highlight json %}
{ "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "data": {
    "url": "https://raw.githubusercontent.com/vega/vega/master/docs/data/sp500.csv"
  },
  "vconcat": [{
    "width": 480,
    "mark": "area",
    "encoding": {
      "x": {
        "field": "date",
        "type": "temporal",
        "scale": {"domain": {"selection": "brush"}},
        "axis": {"title": ""}
      },
      "y": {"field": "price", "type": "quantitative"}
    }
  }, {
    "width": 480,
    "height": 60,
    "mark": "area",
    "selection": {
      "brush": {"type": "interval", "encodings": ["x"]}
    },
    "encoding": {
      "x": {
        "field": "date",
        "type": "temporal"
      },
      "y": {
        "field": "price",
        "type": "quantitative",
        "axis": {"grid": false}
      }
    }
  }]
}
{% endhighlight %}
