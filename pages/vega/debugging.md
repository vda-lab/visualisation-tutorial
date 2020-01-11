---
title: Building complex visualisations and debug
keywords: vega
sidebar: vega_sidebar
permalink: vega-debugging.html
folder: vega
---
**TODO**: add start with vega-lite and look at compiled vega

No `console.log()`

### Log, data viewer and signal viewer

### Use vega-lite as starting point

### Web browser console
How to find out that we have to use `activated_datapoint.datum`? I must admit that this took me a while... In the signal viewer in the bottom right of the vega editor you can see that the value for `activated_datapoint` changes from `null` to `(...)` if we mouse over a datapoint. We cannot see what the value actually is. The vega documentation on debugging at [https://vega.github.io/vega/docs/api/debugging/](https://vega.github.io/vega/docs/api/debugging/) tells us that we can access more information if we open the debug console.

To open the debug console in Google Chrome, go to View => Developer => Developer Tools, and then click on `Console`. Type in `VEGA_DEBUG.view.signal('activated_datapoint')` in the console. The output will probably be `null`.

<img src="{{ site.baseurl }}/assets/vega-debug-1.png" width="50%" />

Now type in that command again, but _without pressing enter_. Put your mouse on top of a datapoint (without moving focus away from the console!) and press enter. You should now see something else than `null`. If you click on the small triangle next to the json object you'll expand the object and see that the `datum` key corresponds to the datapoint that we put in. That's why we use `datum === activated_datapoint.datum` as the test.

<img src="{{ site.baseurl }}/assets/vega-debug-2.png" width="50%" />

{:.exercise}
**Exercise** - Can you add an additional test for the fill? You can make a dummy one, e.g. testing if 1 == 1.

{:.exercise}
**Exercise** - Try out what happens if you don't include the `datapoint_is_activated` in the test above. Tip: open the console as describe above in "Note on debugging".
