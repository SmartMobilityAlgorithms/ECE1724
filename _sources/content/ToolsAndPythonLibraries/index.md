# Tools and Python Libraries

## `smart_mobility_utilities` python package

Many of the operations in this book are long and burdensome to code from scratch. Oftentimes, they are highly standardized and can benefit from having a helper function take care of the various intricacies.

`smart_mobility_utilities` is a python package developed for this purpose. You can clone the repo to your local machine, and install it as follows:

````{tab} pip3
```bash
$ cd smart_mobility_utilities
$ pip install -e .
```
````
````{tab} conda

The `conda` version of this package is still under development. In the meantime, you can import the files directly into your project's file structure.
````


## Mapping Libraries

### osmnx

This library was developed by [Geoff Boeing](https://geoffboeing.com/) from the University of Southern California to ease the process of retrieving and manipulating the data from OpenStreetMap, and to make it easier to be interpolated into Python applications. It offers the ability to download the data (filtered) from OSM and returns the network as `networkx` graph data structure. The library is too complicated to be explained fully in a README file, but you can check the [official website](https://osmnx.readthedocs.io/en/stable/#) and follow Professor Boeing's website as he posts regularly on recent updates and trends about osmnx and the field in general.

### OSMPythonTools

[OSMPythonTools](https://github.com/mocnik-science/osm-python-tools) is a well-written package to query OSM services.

### Open layers

If you are developing a web/mobile application and you want to get really fancy with your maps, you have [Open layers](https://openlayers.org/) which is the industry standard for webmaps.

## Graph Libraries

### networkx

This is one of the pillars of Python programming and scientific computing, besides `numpy` and `scipy`. Its main and only goal is supporting graph data structures and the associated algorithms like shortest path and networks flow and optimization. `osmnx` returns the map as `networkx` network so it is possible to use all the library's functions on the maps obtained from OSM. `networkx` has books written explaining its API's and we wholeheartedly recommend [Complex Network Analysis in Python: Recognize - Construct - Visualize - Analyze - Interpret](https://www.amazon.com/Complex-Network-Analysis-Python-Recognize/dp/1680502697) if you want to dive into it. Information about `networkx` is also available [here](https://networkx.github.io/). 

`networkx` has a monopoly over the field of network analysis for many years now, but the scalability of `networkx` may be an issue. If your network has tens of millions of nodes, it can get really ugly because `networkx` is still just a `python` library, and `python` can't handle these millions of nodes and will run out of memory, and give you a segmentation fault.

You can optimize `python` by using `__slots__` instead of `__dict__`, something which is discussed [here](https://stackoverflow.com/questions/472000/usage-of-slots#:~:text=The%20proper%20use%20of%20__,one%20dict%20for%20every%20object.%5D). You can also use arrays or something similar, but then other problems would arise.

Are there any alternatives? In `C++`, you can use [graph-tool](https://graph-tool.skewed.de/), which was built over the [boost-graph](https://www.boost.org/doc/libs/1_64_0/libs/graph/doc/index.html) libraries, or you can use [igraph](https://github.com/igraph) which is written in C. But for these you will need to write your own parser for OpenStreetMaps data and understand its file format. Fortunately, this is not too complicated.


## Geospatial Data Libraries

### GeoPandas
[GeoPandas](https://geopandas.org/) is an extension to pandas that handles geospatial data by extending the datatypes of pandas, and the ability to query and manipulate spatial data. Alternatively, you would need to deal with [spatial databases](https://en.wikipedia.org/wiki/Spatial_database) for these operations, like how to properly and efficiently represent polygons and curved lines and query them without too much overhead (for database folks, the indexing of spatial data is different than normal data).


## Shapefile Creation and Map Editing

### QGIS

[QGIS](https://www.qgis.org/en/site/) is a free and open-source cross-platform desktop geographic information system application that supports viewing, editing, and analysis of geospatial data. 

### GeoJSON

[GeoJSON](https://geojson.io/) is a fast, simple tool to create, change, and publish maps.


## Geospatial Data Visualization 

There are <b>many</b> libraries for visualization, but we are mainly using [folium](https://python-visualization.github.io/folium/) and [ipyleaflet](https://ipyleaflet.readthedocs.io/en/latest/). Both of them are just wrappers around [leaflet.js](https://github.com/Leaflet/Leaflet), which is the go-to library for any kind of map visualization in almost all web and mobile applications.

Both of `ipyleaflet` and `folium` were created to serve the same purpose, and you don't need to dwell so much on how to use them if you don't want to, as we have provided wrappers around them in  `utilities/utils/viz.py`. This contains two functions: one for drawing a map with our graph overlaid on it, and and the other function is for drawing a route between two places/nodes with markers marking the source and destination. At the very least, you should be able to recognize the differences between the two wrappers. `folium` is much more lightweight than `ipyleaflet`, but on the other hand `ipyleaflet` has more options and very niche capabitilies. `ipyleaflet` doesn't work on Google Colab, unlike `folium`; see [googlecolab/colabtools#60](https://github.com/googlecolab/colabtools/issues/60) for more details. 

There are other visualization libraries that you should be aware of: 

* [hvplot](https://hvplot.holoviz.org/user_guide/Geographic_Data.html), if you want to get going through your analysis with geopandas and dataframes and all that. You should be aware of the significance of working with vanilla [GeoPandas](https://geopandas.org/), and that `osmnx` [supports that](https://osmnx.readthedocs.io/en/stable/osmnx.html#module-osmnx.projection) and yields two dataframes: one for all your nodes and one for all the edges.

* [mplleaflet](https://github.com/jwass/mplleaflet), which is another `leaflet`-based library, but it plays really nicely with `matplotlib`.

* [deck.gl](https://deck.gl/)

* [kepler.gl](https://kepler.gl/)

* [Google Data Studio](https://datastudio.google.com/)


## Geospatial Data Analysis

### shapely

[Shapely](https://pypi.org/project/Shapely/) is a BSD-licensed Python package for manipulation and analysis of planar geometric objects. It provides us with datatypes to represent geometric objects that geopandas exploits to represent spatial data.

### PySAL

[PySAL](https://pysal.org/) or Python Spatial Analysis Library is an open source cross-platform library for geospatial data science with an emphasis on geospatial vector data written in Python. 

### GeoDa

[GeoDa](https://geodacenter.github.io/) is a free and open source software tool that serves as an introduction to spatial data science. It is designed to facilitate new insights from data analysis by exploring and modeling spatial patterns.

## Geocoding

### GeoPy

[GeoPy](https://geopy.readthedocs.io/en/stable/#)  is a Python client for several popular geocoding web services.


### nominatim

[nominatim](https://geopy.readthedocs.io/en/stable/#nominatim) is used to look up a location from a textual description (the official website description). This is called geocoding and decoding, which is translating address of a location to its coordinates (and vice-versa).

### Photon Geocoder

[photon](https://github.com/komoot/photon) is an open source geocoder built for OpenStreetMap data.

### Other geocoders

[Open Data and Open Source Geocoders](https://blog.batchgeo.com/open-data-open-source-geocoders/)


## Routing Libraries 

### osrm

For some problems, determining the route between multiple points is not the main focus, and it is acceptable to use a pre-generated route. [OSRM](http://project-osrm.org/) does exactly that; it is a routing engine with an API that you feed with coordinates, and in return it gives you the fastest route between them. It has other useful capabilities like doing Travelling Salesman and solving all pairs shortest path.

### Valhalla

[Valhalla](https://valhalla.readthedocs.io/en/latest/)'s routing service (a.k.a. turn-by-turn), is an open-source routing service that lets you integrate routing and navigation into a web or mobile application.

### Openrouteservice

The [openrouteservice - ORS](https://openrouteservice.org/) provides global spatial services by consuming user-generated and collaboratively collected free geographic data directly from OpenStreetMap. It is highly customizable, performant and written in Java.

### Routing

Geofabrik operates a [routing service](https://www.geofabrik.de/data/routing.html) based on [OSRM](http://project-osrm.org/). OSRM makes use of state-of-the-art routing algorithms and can compute routes across Europe within milliseconds. The engine supports the following features: via points, turn restrictions and turn maneuvers.

### traffic per edge and Open traffic

Do you want traffic data beyond just max speed and duration? Check out [traffic per edge](https://github.com/Project-OSRM/osrm-backend/wiki/Traffic) or [Open traffic](https://github.com/opentraffic).


#### Note

Most of these libraries use coordinates as input and/or output, but please take into account that some of them accept the coordinates as (longtitude, latitude) and others as (latitude, longtitude). 

## Others 

### tqdm

[tqdm](https://github.com/tqdm/tqdm) helps us to see the progress of our algorithm while it is running. We use it in all of the other repositories to track the speed of the algorithm in traversing the given map, and how many nodes are expanded per second. It works on any python iterable structure.

