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
This article will illustrate a step-by-step process to create an interactive web dashboard. A web dashboard consists of three parts, web client, web server and database. The function of each of these components will be discussed in more detail in the [architecture section](#architecture). This dashboard was developed using HTML5, JavaScript and CSS. The main frameworks and libraries used are: 
{: style="text-align: justify"}

### Front-End
1. [jQuery](https://api.jquery.com/)

2. [Bootstrap](https://getbootstrap.com)

3. [Leaflet](https://leafletjs.com)

4. [Plotly](https://plotly.com)

### Back-End
1. API Endpoint

2. GeoJSON

<figure>
    <img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/Dashboard.png" alt="dashboard user view">
    <figcaption style="text-align: center">Chicago crime dashboard main user interface (ux).</figcaption>
</figure>

## Data
This project uses the following data-set:

1. **[Chicago Crime](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2/data)**: API endpoint containing nearly 7 million crime records between 2001 onwards. Each incident recorded at block level containing 22 attributes (e.g. crime type, date and coordinates).

2. **[Chicago Community Area Boundary](https://raw.githubusercontent.com/RandomFractals/ChicagoCrimes/master/data/chicago-community-areas.geojson)**: GeoJSON containing Chicago community area boundary map for the year of 2015.

3. **[Chicago Community Area Population](https://www.chicago.gov/content/dam/city/depts/zlup/Zoning_Main_Page/Publications/Census_2010_Community_Area_Profiles/Census_2010_and_2000_CA_Populations.pdf)**: Population size per community area based on the 2010 census.

## Architecture

This dashboard uses [three-tier architecture](https://en.wikipedia.org/wiki/Multitier_architecture), a client, server and database architecture. In this architecture as shown in the figure below, the web client is responsible for querying the database and returning an HTTP response in for of a GeoJSON object. The HTTP response is processed and manipulated using JavaScript and displayed using HTML in the browser. This architecture allows each tier (i.e. Web, Server and Database) to be developed and maintain independently on a separate platform. This means that any of the three tiers can be replaced or upgraded in response to technological advancements, for example, the release of a new operating system (OS).
{: style="text-align: justify"}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/3_tier.jpg" alt="Three tier architecture">

## Steps


## Graphical User Interface GUI (Results)


## Summary (Final Recommendation)
There are several benefit of deploying an open source dashboard. It's free, highly customisable, and allows anyone with the right skills to visualise and analyse data, without the need for major financial investments. 

**Source code**: available on [github](https://github.com/Geobuddy/Crime-Dashboard).

Here's a bulleted list:
* First issue_term
+ Second issue_term
- Third issue_term

Here's a numbered list:
1. First issue_term
2. Second issue_term
3. Third issue_term

Python code block:
```JavaScript
    import numpy as np

    def test_function():
      z = np.sum(x,y)
      return z
```



Here some inline code `x+y`.

Here's an image:
<img src="{{ site.url }}{{ site.baseurl }}/images/dashboard/Dashboard.png" alt="dashboard user view">


