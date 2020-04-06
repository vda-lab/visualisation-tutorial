---
title: Setting things up
keywords: vega-in-r
sidebar: vega-in-r_sidebar
permalink: /vega-in-r-setting-things-up.html
folder: vega-in-r
series: vega-in-r-series
weight: 1
---

To get this tutorial started, we need, first, to install anaconda, and second, activate an r-reticulate environment using conda. We also need to install vega_datasets using pip and finally, install the R packages reticulate and altair using install.packages() in Rstudio. 
Most of the steps described here are taken from [altair R installation](https://vegawidget.github.io/altair/articles/installation.html). Make sure you are using Python version 3.5 or higher to comply to the system requirements of the altair R package [altair CRAN](https://cran.r-project.org/web/packages/altair/altair.pdf).

First, [install Anaconda](https://www.anaconda.com/distribution/) and after installing Anaconda, open the Anaconda Prompt. 
Update conda:
``` C
conda -V
conda update conda
````

Install the vega datasets that we will be used in this tutorial:
``` C
pip install vega_datasets
```

Next, create and activate a conda environmnet called `r-reticulate`:
``` C
conda create -n r-reticulate
conda activate r-reticulate
```

Open Rstudio IDE and install reticulate. Then, use the conda environment `r-reticulate`:
``` R
install.packages("reticulate")
reticulate::use_condaenv("r-reticulate")
```

Restart Rstudio and then install the altair package:
``` R
install.packages("altair")
```

In Rstudio, use the code below to install the Python packages altair and vega_datasets:
``` R
altair::install_altair()
```

Verify the installation using:
``` R
altair::check_altair()
```

If there is no error on the verification, we are ready to start!
<br/>
The procedure described above should be run only in the beginning. The following times you want to use altair in Rstudio, you only need to call `library("altair")`.




{% include custom/series_vega-in-r_next.html %}
