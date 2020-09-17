---
title: "Chicago Crime Dashboard"
date: 2019-11-18
tags: [dashboard, data visualisation, data analysis]
header:
  overlay_image: "/images/Background.jpg"
excerpt: "Data Science, Dashboard, Data Visualisation"
mathjax: "true"
toc: true
toc_label: "My Table of Contents"
toc_icon: "file-alt"
---
## How to create a dashboard?
This article will illustrate a step-by-step process to create an interactive web dashboard. A web dashboard consists of three parts, a web client, web server and database. The function of each of these components are be discussed in more detail in the [architecture section](#architecture). This dashboard was developed using HTML5, JavaScript and CSS. The main frameworks and libraries used are: 
{: style="text-align: justify"}
**Front-End**
1. [jQuery](https://api.jquery.com/)
2. [Bootstrap](https://getbootstrap.com)
3. [Leaflet](https://leafletjs.com)
4. [Plotly](https://plotly.com)

**Back-End**
1. API Endpoint
2. GeoJSON

## Data
The data used in this project comprises the crime data sourced from the city of Chicago public data, an area boundary map in GeoJSON format and the population data. 
{: style="text-align: justify"} 
The source of the dataset is the following:
1. **[Chicago Crime](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2/data)**: API endpoint containing nearly 7 million crime records between 2001 onwards. Each incident recorded at block level containing 22 attributes (e.g. crime type, date and coordinates).
2. **[Chicago Community Area Boundary](https://raw.githubusercontent.com/RandomFractals/ChicagoCrimes/master/data/chicago-community-areas.geojson)**: GeoJSON containing Chicago community area boundary map for the year of 2015.
3. **[Chicago Community Area Population](https://www.chicago.gov/content/dam/city/depts/zlup/Zoning_Main_Page/Publications/Census_2010_Community_Area_Profiles/Census_2010_and_2000_CA_Populations.pdf)**: Population size per community area based on the 2010 census.

## Architecture
This dashboard uses [three-tier architecture](https://en.wikipedia.org/wiki/Multitier_architecture), a client, server and database architecture. In this architecture as shown in the figure below, the web client is responsible for querying the database and returning an HTTP response in of a GeoJSON object. The HTTP response is processed and manipulated using JavaScript and displayed using HTML in the browser. This architecture allows each tier (i.e. Web, Server and Database) to be developed and maintain independently on a separate platform. This means that any of the three tiers can be replaced or upgraded in response to technological advancements, for example, the release of a new operating system (OS).
{: style="text-align: justify"}

<figure>
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/3_tier.jpg" alt="Three tier architecture">
    <figcaption style="text-align: center">This figure illustrates the three-tier architecture fundamental to all modern web-based application. This architecture comprises a web client, a server and a database. </figcaption>
</figure>

## Steps
### Front-End Design
The first step of this project was to define the layout of the user interface. The layout used for this project was the created using a template from [material design](https://material.io). The main component of graphical user interface are the sidebar comprising the filtering parameters (e.g. Offence Group and Dates), a map and collapsible buttons that display graphs when clicked.
{: style="text-align: justify"}

<figure>
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/main.png" alt="UX">
    <figcaption style="text-align: center">This figure illustrates the Chicago Crime Dashboard graphical user interface.</figcaption>
</figure>

<script style="max-height: 250px; overflow-y: visible" src="https://gist.github.com/Geobuddy/7179e400f40c018c557a14d1854f8fe4.js"></script>

### Back-End Implementation
#### Data Request
The initial process in this development consists in loading the data resources from the API endpoints and local file. The data is loaded through a jQuery AJAX request. An AJAX stands for Asynchronous JavaScript And XML. The jQuery AJAX method uses a browser built-in XMLHttpRequest object to request data from a web server, processes the returned data using JavaScript and displays in a HTML DOM. This whole process occurs asynchronously where data is exchanged with a web server in the back-end. This enables to update parts of a web site, without the need to reload the whole page. Figure 5 shows the implantation of AJAX to load the data from the API endpoints and local JSON file.
{: style="text-align: justify"}

<script style="max-height: 250px; overflow-y: visible" src="https://gist.github.com/Geobuddy/6d48395ce0475ff0bf24a82e4b7996cf.js"></script>

#### Data Transformation
In order to display the crime rate into to a choropleth map we needed transform the data. This requires merging of the crime data and population data into the boundary GeoJSON (Fig. 6). The crime and the population data were merged into the boundary GeoJSON because the paths (i.e. MultyPolygon) to construct the choropleth layer are generated from this dataset. We created two monster arrays for the crime data and the population data which were in turn bind to the boundary GeoJSON path elements all at the same time. In order to bind to data sets we need to determine common proprieties on both data sets. In this particular example we used the community area number which was available in all three data sets. For example, for each community area number in the Chicago crime GeoJSON, we matched the same number on the Chicago boundary GeoJSON. Then we selected the Chicago crime data value we want to bind and merged it under myBoundary[j]. properties. Value, which can later when plotting the map. Similar process was carried to bind the population data set. Having the crime count and the population size per community area enable the calculation of the crime rate per community area. 
{: style="text-align: justify"}

<script style="max-height: 250px; overflow-y: visible" src="https://gist.github.com/Geobuddy/e15fc2a050c339c5ebae625ff31b4c20.js"></script>

## Graphical User Interface GUI (Results)

<figure>
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/dashboard.png" alt="Choropleth Map">
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/heatmap.png" alt="Heat Map">
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/clustermap.png" alt="Cluster Map">
    <figcaption style="text-align: center">This figure illustrates different crime mapping techniques implement in web crime platform. Choropleth map, Heatmap and Cluster map. </figcaption>
</figure>

## Summary (Final Recommendation)
There are several benefit of deploying an open source dashboard. It's free, highly customisable, and allows anyone with the right skills to visualise and analyse data, without the need for major financial investments. 
{: style="text-align: justify"}

**Source code**: available on [github](https://github.com/Geobuddy/Crime-Dashboard).
3

Python code block:
```JavaScript
    import numpy as np

    def test_function():
      z = np.sum(x,y)
      return z
```


