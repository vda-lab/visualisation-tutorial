---
title: Panel layout
keywords: holoviz
sidebar: holoviz_sidebar
toc: false
permalink: holoviz-panel-layout.html
folder: holoviz
series: holoviz-series
weight: 5
---
We can layout different panes into a panel with rows, columns or tabs. For example:

```python
pn.Column(pn.pane.Markdown("# My title"),
          pn.pane.Markdown("Some text"))
```

We can make the layout more complex by combining different tags:
```python
pn.Column(pn.pane.Markdown("# My title"),
          pn.Row(pn.pane.Markdown("Some text"),
                 pn.pane.Markdown("Some other text")))
```

...and combining different types of panes:
```python
pn.Column(pn.pane.Markdown("# My title"),
          pn.Row(pn.pane.Markdown("The first hit when I search google images for the text 'panel'"),
                 pn.pane.JPG("https://5.imimg.com/data5/PA/LN/MY-13921/dol-starter-panel-500x500.jpg")))
```

![]({{ site.baseurl }}/assets/holoviz-panel-picture.png)

{% include custom/series_holoviz_next.html %}
