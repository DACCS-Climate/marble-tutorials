-[The Marble Platform](#marble-platform)
-[Nodes](#nodes)
- [Main Areas of the Platform](#main-areas)
  - [The Homepage](#homepage)
  - [JupyterLab](#jupyterlab)
  - [The Data Catalog](#data-catalog)
  - [The Web Processing Services](#webservices)


## <a id="marble-platform"></a>The Marble Platform

Marble provides the perfect podium for climate researchers to store and share their work. 
A climate researcher's findings can be stored on the Marble Platform where it will be accessible by the public.

The Marble Platform is made up of several servers (nodes) connected to each other. 
Each node provides data storage, and web services for managing workflows and processing data.  Logging into one node 
allows access to the resources of all the nodes on the network.   

## <a id="nodes"></a>Nodes

A node is a server with specialized software installed and is hosted by a partner in the Marble network.
There are currently four nodes in the Marble network, and each node has a different focus - the Ouranos PAVICS node 
focuses on climate analysis, the Computer Research Institute of Montreal (CRIM) node focuses on machine learning, 
the U of T node focuses on climate research, and the Pacific Climate Impacts Consortium (PCIC) node focuses on data 
management and storage.

When using Marble you are choosing one of these nodes on which to perform data analysis, but you will have access to
the resources of all of the nodes on the network. 

## <a id="main-areas"></a>Main Areas of the Platform

### <a id="homepage"></a>The Homepage

The [Marble Climate homepage](https://marbleclimate.com/index.html) is the main point of access to the Marble platform 
and main source of information.

### <a id="jupyterlab"></a>JupyterLab
JupyterLab will be the main area where you will be doing your work.  Start a notebook by clicking the `Python 3` button or `birdy` button (if available) under the Notebook section. 

![Jupyter Notebook Buttons](images/getting-started/jupyter-notebook-buttons.png)

### <a id="data-catalog"></a>The Data Catalog
The STAC Browser is the interface to the vast data catalog stored on each node.  

From the [Marble Climate](https://marbleclimate.com) website. Click the `Data Catalog` link.  On the **Data Catalog** page select the node whose data you wish to browse.  You will then be taken to the STAC Browser for that node.

![STAC Browser Home](images/getting-started/stac-browser-home.png)

### <a id="webservices"></a>The Web Processing Services
The [Web Processing Services](https://marbleclimate.com/remote-processing.html) are provided by the 
[Bird House](https://github.com/bird-house).  Each "bird" in the bird house provides a specific service tailored for climate research.

- [Finch](https://pavics-sdi.readthedocs.io/projects/finch/en/latest/) provides climate indicator processing
- [Raven](https://pavics-sdi.readthedocs.io/projects/raven/en/latest/) provides hydrological modelling and analytics
- [Hummingbird](https://birdhouse-hummingbird.readthedocs.io/en/latest/index.html) provides metadata checks
- [Weaver](https://pavics-weaver.readthedocs.io/en/latest/) allows entire workflows to be executed remotely