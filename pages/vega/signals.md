---
title: Signals
keywords: vega
sidebar: vega_sidebar
permalink: vega-signals.html
folder: vega
series: vega-series
weight: 15
---
So once an event occurs, the corresponding signal changes. In the example above, every time the mouse is moved, the `event.x` (i.e. the horizontal position on the screen of where the event (i.e. the moving mouse) occurred) is made available to Vega through the `mouseX` variable/signal.

This `mouseX` can then be used in the specification for the `marks`, `scales`, etc.

Different patterns for signals:

```json
{
  "name": "colourSelector",
  "bind": {"input": "select", "options": ["steelblue","red"]
}
```

```json
{
  "name": "mouseX",
  "on": [ {"events":"mousemove", "update": "event.x"} ]
}
```

**TODO**: others?

{% include custom/series_vega_next.html %}
