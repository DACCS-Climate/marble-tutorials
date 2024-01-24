# GUI Search

Each node in the Marble network include a GUI application called [STAC Browser](https://github.com/radiantearth/stac-browser) that allows you to 
explore the STAC catalog of data available on that node. This application is available at `https://host-url/stac-browser`, where
`host-url` is the URL of the Marble node. For example, for the Marble node 'Red Oak' available at 'https://daccs.cs.toronto.edu/',
the STAC Browser can be accessed at [](https://daccs.cs.toronto.edu/stac-browser).

In this tutorial, you will get an introduction to the STAC Browser, how to navigate within the Browser, how to perform search,
and how to get access links to data. You will also learn about the limitations of the GUI, which will segway into the 
[next section](pystac-client.ipynb) where a programtic way to interact with the STAC Catalog is introduced.

## GUI overview

In this tutorial, we'll use **Red Oak** node as an example. Start by navigating to the [STAC Browser on Red Oak](https://daccs.cs.toronto.edu/stac-browser) in a new tab; 
you should see a screen similar to what is shown below.

```{note}
It is important to keep in mind that the data catalog on Marble is continuously evolving and so the STAC Browser view that you see 
at any time could be different from that shown in this tutorial. However, the differences will only conern the 
content of the data catalog, and not the application itself. If any interface or functionality changes to the STAC Browser itself renders 
aspects of this tutorial outdated, then the tutorial will be updated to reflect those changes.
```

![GUI Home Page](images/gui-home.png)

1. The first thing you will notice is the bold text at the top left of the page. The STAC Browser uses this part of the page to display
    the "title" of the page. In this case, since you are at the root of the STAC Catalog, the appropriate title is the
    _title_ field of the [root catalog](https://daccs.cs.toronto.edu/stac).
2. Immediately below the title is an area that will contain various navigation options for going back up the catalog hierarchy, as well as the "Browse" and "Search" tabs. Since we are at the
    root of the catalog no navigation options are needed here, and you only see the two tabs.
3. The "Description" section will display the description for the page you are on. In this case it is displaying the _description_ field
    of the [root catalog](https://daccs.cs.toronto.edu/stac).
4. The "Additional resources" section includes links to the description and documentation of the STAC API underpinning the STAC service.
    If you are unfamiliar with what this means, then this is not meant for you and you can safely ignore the content.
5. On the top-right of the screen you always see the "Source" and "Share" tabs. Clicking on the Source tab will show you the version of 
    [stac specification](https://github.com/radiantearth/stac-spec) that is being used and whether or not the STAC data displayed on that
    page is valid according to the STAC standards and extensions used (see image below). Crucially, it provides a quick access to the STAC URL 
    that contains the STAC metadata that is being parsed and displayed by the Browser.
    ![Source Tab](images/source-tab.png)
6. Finally, in the lower part of the document, you will see the "Catalogs" section. This section provides "lists" all the 
    child STAC collections, or catalogs, on the node, as well as functionality to sort and search for a catalog by name. In the above image, 
    there is only only collection, namely the "CMIP6" collection.

```{note}
Although the root of a STAC catalog has to be a ["catalog"](https://github.com/radiantearth/stac-spec/blob/master/catalog-spec/catalog-spec.md), 
there is very little practical difference whether the children of the root catalog (or their own children, _ad infinitum_) are
catalogs or ["collection"](https://github.com/radiantearth/stac-spec/blob/master/collection-spec/collection-spec.md). In this tutorial, 
we'll always refer to any child catalog/collection as a "collection", and to the root catalog as "catalog".
```

## Browsing a collection
Clicking on a collection from the catalog root will take you into the view that exposes important information about the 
collection.

![Collection View](images/cmip6_collection.png)


## Retrieving access links


## GUI Limitations