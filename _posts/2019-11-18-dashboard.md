---
title: "Chicago Crime Dashboard"
date: 2019-11-18
tag: [dashboard, data visualisation, data analysis]
header:
  overlay_image: "/images/Background.jpg"
excerpt: "Data Science, Dashboard, Data Visualisation"
mathjax: "true"
toc: true
toc_label: "My Table of Contents"
toc_icon: "file-alt"
---
## How to create a dashboard?
This article will illustrate a step-by-step process to create an interactive web dashboard. The deployed version of this dashboard is available in this [link](https://www.crime-dashboard.herokuapp.com/index.html) on heroku. A web dashboard consists of three parts, a web client, a web server and a database. The function of each of these components are to be discussed in more detail in the [architecture section](#architecture). This dashboard was developed using HTML5, JavaScript and CSS. The main frameworks and libraries used are: 
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
This dashboard uses [three-tier architecture](https://en.wikipedia.org/wiki/Multitier_architecture), a client, server and database architecture. In this architecture as shown in the figure below, the web client is responsible for querying the database and returning an HTTP response in the form of a GeoJSON object. The HTTP response is processed and manipulated using JavaScript and displayed using HTML in the browser. This architecture allows each tier (i.e. Web, Server and Database) to be developed and maintained independently on a separate platform. This means that any of the three tiers can be replaced or upgraded in response to technological advancements, for example, the release of a new operating system (OS).
{: style="text-align: justify"}

<figure>
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/layers.png" alt="Three tier architecture">
    <figcaption style="text-align: center">This figure illustrates the three-tier architecture fundamental to all modern web-based application. This architecture comprises a web client, a server and a database. </figcaption>
</figure>

## Steps
### Front-End Design
The first step of this project was to define the layout of the user interface. The layout used for this project was the created using a template from [material design](https://material.io). The main component of the graphical user interface are the sidebar comprising the filtering parameters (e.g. Offence Group and Dates), a map and collapsible buttons that display graphs when clicked.
{: style="text-align: justify"}

<figure>
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/main.png" alt="UX">
    <figcaption style="text-align: center">This figure illustrates the Chicago Crime Dashboard graphical user interface.</figcaption>
</figure>

### Back-End Implementation
#### Data Request
The initial process in this development consists in loading the data resources from the API endpoints and local file. The data is loaded through a jQuery AJAX request. An AJAX stands for Asynchronous JavaScript And XML. The jQuery AJAX method uses a browser built-in XMLHttpRequest object to request data from a web server, processes the returned data using JavaScript and displays in a HTML DOM. This whole process occurs asynchronously where data is exchanged with a web server in the back-end. This enables to update parts of a web site, without the need to reload the whole page. The gist below shows the implantation of AJAX to load the data from the API endpoints and local JSON file.
{: style="text-align: justify"}

<script style="max-height: 150px; overflow-y: scroll" src="https://gist.github.com/Geobuddy/6d48395ce0475ff0bf24a82e4b7996cf.js"></script>

#### Data Transformation
In order to display the crime rate into to a choropleth map we needed transform the data. This requires merging of the crime data and population data into the boundary GeoJSON map. The crime and the population data were merged into the boundary GeoJSON because the paths (i.e. MultyPolygon) to construct the choropleth layer are generated from this dataset. We created two monster arrays for the crime data and the population data which were in turn bind to the boundary GeoJSON path elements all at the same time. In order to bind to data sets we need to determine common proprieties on both data sets. In this particular example we used the community area number which was available in all three data sets. For example, for each community area number in the Chicago crime GeoJSON, we matched the same number on the Chicago boundary GeoJSON. Then we selected the Chicago crime data value we want to bind and merged it under myBoundary[j]. properties. Value, which can later when plotting the map. Similar process was carried to bind the population data set. Having the crime count and the population size per community area enable the calculation of the crime rate per community area. 
{: style="text-align: justify"}

<script style="max-height: 150px; overflow-y: scroll" src="https://gist.github.com/Geobuddy/e15fc2a050c339c5ebae625ff31b4c20.js"></script>

## Graphical User Interface GUI
### Maps
In this project, we have used Open Street Map (OSM) and Carto DB basemaps which can be displayed by check the according box in the leaflet layer control located on the top right corner of the map. The basemaps can be overlain by three distinct mapping layers. Three distinct mapping visualisation techniques were adopted, a choropleth map , a heatmap and a cluster map. A mouse pointing highlight function is available in the choropleth map enabling the user to visualise information dynamically about the chosen community area. This information is displayed in an information box located on the top right corner of the map.
{: style="text-align: justify"}

<figure>
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/dash.png" alt="Choropleth Map">
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/heatmap.png" alt="Heat Map">
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/clustermap.png" alt="Cluster Map">
    <figcaption style="text-align: center">This figure illustrates different crime mapping techniques implement in web crime platform. Choropleth map, Heatmap and Cluster map (top to bottom).</figcaption>
</figure>

### Charts
In this project, we generated charts using the plotlyJS library. The charts and graphs provided to give the user a different insight into the data besides the map. Four plots are included alongside the map in the main section, a crime count, a time-series, an average monthly crime and arrest and domestic bar graph. Crime count graph shows the total number of incidents recorded within a defined time frame. The time-series illustrates the number of incidents recorded per month within a set timeframe. The average monthly crime count shows the average distribution of the incidents per month over a define timeframe. Lastly, pie charts in shows the percentage of arrest and domestic cased for a specific crime within a particular time frame. 
{: style="text-align: justify"}

<figure>
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/charts.png" alt="Charts">
    <figcaption style="text-align: center">This figure illustrates dynamic analytical graphs displaying crime count, crime time-series, average monthly crime plot and arrest and domestic count.</figcaption>
</figure>

## Summary
There are several benefits of deploying an open source dashboard. It's free, highly customisable, and allows anyone with the right skills to visualise and analyse data, without the need for major financial investments. For instance, this solution can contribute to crime fighting in developing countries where financial and technological resources are often limited.
{: style="text-align: justify"}

**Source code**: available on [github](https://github.com/Geobuddy/Crime-Dashboard).
