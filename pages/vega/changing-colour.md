---
title: Changing colour
keywords: vega
sidebar: vega_sidebar
permalink: vega-changing-colour.html
folder: vega
---
The points in the plot above are blue. In vega-lite, we'd just add `"color": {"value": "red"}` to the `encoding` section to change this. In vega, however, the keyword `color` is not recognised. Instead, a distinction is made between `fill` and `stroke`. `fill` corresponds to the area of the point itself; `stroke` refers to the _outline_ of the point (the _circle_).

{:.exercise}
**Exercise** - Change the colour of the points to red.

{:.exercise}
**Exercise** - Change the colour of the point _outline_ to green.

{:.exercise}
**Exercise** - In the previous exercise, you'll see that the outline is very thin. Check the documentation for a `symbol` at [https://vega.github.io/vega/docs/marks/symbol/](https://vega.github.io/vega/docs/marks/symbol/) to find out how to make this line thicker.

{:.exercise}
**Exercise** - Change the shape of the symbol from a circle to a something rectangular. Again: check the [documentation](https://vega.github.io/vega/docs/marks/symbol/).

{:.exercise}
**Exercise** - Let's try to have the colour of each point be dependent on the data itself. Change the data so that each datapoint also has some colour assigned to it (e.g. `{"x": 15, "y": 8, "c": "yellow"},`) and adjust the encoding to use this colour.
