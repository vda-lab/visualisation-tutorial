---
title: Panel is reactive
keywords: holoviz
sidebar: holoviz_sidebar
toc: false
permalink: holoviz-panel-is-reactive.html
folder: holoviz
series: holoviz-series
weight: 7
---
One of the strong points of panel is that is reactive. As we described in the [vega tutorial]({{ site.baseurl }}/vega-advanced-interaction.html), in a reactive program any change in a variable will automatically be reflected in other variables that depend on it.

Let's create a small panel with a title and a bit of text:
```python
title = pn.pane.Markdown("# This is my title")
text = pn.pane.Markdown("This is the text")
pn.Column(title, text)
```

As expected, this is what we get:

-----
# This is my title
This is the text

-----

The `title` variable is much more than just a bit of text. You can see that is you check what methods are available on it: write `title.` (with the period) and try tab-completion. Calling `title.object` will give you the text contained in the variable: `# This is my title`. We can use that to change the text:

```python
title.object = "# This is my new title"
```

Now automatically, the previous output will be changed into

---
# This is my new title
This is the text

---

So you don't have to re-run cells in the notebook to update their output, and any data streams will be dynamically reflected.


{% include custom/series_holoviz_next.html %}
