---
title: Installation and jupyter notebook
keywords: holoviz
sidebar: holoviz_sidebar
toc: false
permalink: holoviz-installation-and-jupyter-notebook.html
folder: holoviz
series: holoviz-series
weight: 1
---
We'll start from the assumption that you have jupyter notebooks installed. If not, see [here](https://jupyter.org/install) for the instructions. It's basically running `pip install notebook`, and then `jupyter notebook` to start the server.

### Installation of panel and param
Panel and Param can be installed in the same way as jupyter notebook was with `pip`. Depending on when you're following this tutorial you will have to install `panel` directly from github instead of the regular way because some vega-related bugs were recently fixed that might not have made it in the latest release.

On the command line, run:
* `pip install param`
* `pip install git+https://github.com/holoviz/panel.git`

You'll also need to install the `vega` library:
* `pip install vega`

To start a notebook, run `jupyter notebook`.

{% include custom/series_holoviz_next.html %}
