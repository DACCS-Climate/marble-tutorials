# Getting Started

```{contents}
```


## The Marble Platform

## Nodes

When using Marble you are choosing one of these nodes on which to perform data analysis, but you will have access to
the resources of all of the nodes on the network. 

## Main Areas of the Platform

### The Homepage

The [Marble Climate homepage](https://marbleclimate.com/index.html) is the main point of access to the Marble platform 
and main source of information.

### JupyterLab
JupyterLab will be the main area where you will be doing your work.  Start a notebook by clicking the `Python 3` button or `birdy` button (if available) under the Notebook section. 

![Jupyter Notebook Buttons](images/getting-started/jupyter-notebook-buttons.png)

### The Data Catalog
The STAC Browser is the interface to the vast data catalog stored on each node.  

From the [Marble Climate](https://marbleclimate.com) website. Click the `Data Catalog` link.  On the **Data Catalog** page select the node whose data you wish to browse.  You will then be taken to the STAC Browser for that node.

![STAC Browser Home](images/getting-started/stac-browser-home.png)

### The Web Processing Services
The [Web Processing Services](https://marbleclimate.com/remote-processing.html) are provided by the 
[Bird House](https://github.com/bird-house).  Each "bird" in the bird house provides a specific service tailored for climate research.

- [Finch](https://pavics-sdi.readthedocs.io/projects/finch/en/latest/) provides climate indicator processing
- [Raven](https://pavics-sdi.readthedocs.io/projects/raven/en/latest/) provides hydrological modelling and analytics
- [Hummingbird](https://birdhouse-hummingbird.readthedocs.io/en/latest/index.html) provides metadata checks
- [Weaver](https://pavics-weaver.readthedocs.io/en/latest/) allows entire workflows to be executed remotely