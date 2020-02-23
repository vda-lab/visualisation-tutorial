---
title: Sharing dashboards
keywords: holoviz
sidebar: holoviz_sidebar
toc: false
permalink: holoviz-sharing-dashboards.html
folder: holoviz
series: holoviz-series
weight: 8
---
Panel has another neat trick: it can create a dashboard that is separate from the whole jupyter notebook interface.

In the previous section, we created a dashboard with a title, some text and a plot:
```python
pn.Column(pn.pane.Markdown("# This is a horizontal barchart"),
          pn.Row(
                 pn.panel("This barchart with 4 categories shows us how we can combine different panes, including vega plots"),
                 pn.pane.Vega(spec)
          ))
```

This code was embedded in the rest of the notebook, so actually looked like this:

![]({{ site.baseurl }}/assets/holoviz-dashboard-in-notebook.png)

Obviously, this is good enough if we're still in the developing phase, but at some point, we will want to have a cleaner solution.

### Sharing on your own computer
Nothing could be simpler: just by add `.show()` to the code above, jupyter notebook opens a new window with just this dashboard.

```python
pn.Column(pn.pane.Markdown("# This is a horizontal barchart"),
          pn.Row(
                 pn.panel("This barchart with 4 categories shows us how we can combine different panes, including vega plots"),
                 pn.pane.Vega(spec)
          )).show()
```

![]({{ site.baseurl }}/assets/holoviz-dashboard-in-separate-window.png)

This starts a new notebook process on your computer and opens a new browser tab with just the dashboard.

### More permanently
In some cases, however, you want to make the dashboard available to a bigger group of people and just want to have it run on some server. In that case we cannot run the notebook interactively and use another solution.

This is a two-step process:
1. Instead of `.show()`, call the method `.servable()` on the dashboard that you want to make available. This will not do anything while you are still in the notebook.
1. When you have saved the notebook, run `panel serve --show my_notebook.ipynb` on the command line. This will run the complete jupyter notebook in the backend, take the dashboard that can be identified with the `.servable()` method, and create a new interface.

This is the output when I run this command:

![]({{ site.baseurl }}/assets/holoviz-servable.png)

This output shows us that the dashboard is running on http://localhost:5006/minimal_vega where other people can access it (obviously replace `localhost` with the correct IP number).

If you have `.servable()` on more than one dashboard, these will all be included.

{% include custom/series_holoviz_next.html %}
