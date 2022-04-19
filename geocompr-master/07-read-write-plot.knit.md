# Geographic data I/O {#read-write}

## Prerequisites {-}

This chapter requires the following packages:


```r
library(sf)
library(raster)
library(dplyr)
library(spData)
```

## Introduction

This chapter is about reading and writing geographic data.
Geographic data *import* is essential for geocomputation\index{geocomputation}: real-world applications are impossible without data.
For others to benefit from the results of your work, data *output* is also vital.
Taken together, we refer to these processes as I/O, short for input/output.

Geographic data I/O is almost always part of a wider process.
It depends on knowing which datasets are *available*, where they can be *found* and how to *retrieve* them.
These topics are covered in Section \@ref(retrieving-data), which describes various *geoportals*, which collectively contain many terabytes of data, and how to use them.
To further ease data access, a number of packages for downloading geographic data have been developed.
These are described in Section \@ref(geographic-data-packages).

There are many geographic file formats, each of which has pros and cons.
These are described in Section \@ref(file-formats).
The process of actually reading and writing such file formats efficiently is not covered until Sections \@ref(data-input) and \@ref(data-output), respectively.
The final Section \@ref(visual-outputs) demonstrates methods for saving visual outputs (maps), in preparation for Chapter \@ref(adv-map) on visualization.

## Retrieving open data {#retrieving-data}

\index{open data}
A vast and ever-increasing amount of geographic data is available on the internet, much of which is free to access and use (with appropriate credit given to its providers).
In some ways there is now *too much* data, in the sense that there are often multiple places to access the same dataset.
Some datasets are of poor quality.
In this context, it is vital to know where to look, so the first section covers some of the most important sources.
Various 'geoportals' (web services providing geospatial datasets such as [Data.gov](https://catalog.data.gov/dataset?metadata_type=geospatial)) are a good place to start, providing a wide range of data but often only for specific locations (as illustrated in the updated [Wikipedia page](https://en.wikipedia.org/wiki/Geoportal) on the topic).

\index{geoportals}
Some global geoportals overcome this issue.
The [GEOSS portal](http://www.geoportal.org/) and the [Copernicus Open Access Hub](https://scihub.copernicus.eu/), for example, contain many raster datasets with global coverage.
A wealth of vector datasets can be accessed from the National Aeronautics and Space Administration agency (NASA), [SEDAC](http://sedac.ciesin.columbia.edu/) portal and the European Union's [INSPIRE geoportal](http://inspire-geoportal.ec.europa.eu/), with global and regional coverage.

Most geoportals provide a graphical interface allowing datasets to be queried based on characteristics such as spatial and temporal extent, the United States Geological Services' [EarthExplorer](https://earthexplorer.usgs.gov/) being a prime example.
*Exploring* datasets interactively on a browser is an effective way of understanding available layers.
*Downloading* data is best done with code, however, from reproducibility and efficiency perspectives.
Downloads can be initiated from the command line using a variety of techniques, primarily via URLs and APIs\index{API} (see the [Sentinel API](https://scihub.copernicus.eu/twiki/do/view/SciHubWebPortal/APIHubDescription) for example).
Files hosted on static URLs can be downloaded with `download.file()`, as illustrated in the code chunk below which accesses US National Parks data from: [catalog.data.gov/dataset/national-parks](https://catalog.data.gov/dataset/national-parks):


```r
download.file(url = "http://nrdata.nps.gov/programs/lands/nps_boundary.zip",
              destfile = "nps_boundary.zip")
unzip(zipfile = "nps_boundary.zip")
usa_parks = st_read(dsn = "nps_boundary.shp")
```

## Geographic data packages

\index{data packages}
A multitude of R packages have been developed for accessing geographic data, some of which are presented in Table \@ref(tab:datapackages).
These provide interfaces to one or more spatial libraries or geoportals and aim to make data access even quicker from the command line.

<!-- add sentinel2 package as soon as it is published on CRAN https://github.com/IVFL-BOKU/sentinel2-->
<table class="table" style="margin-left: auto; margin-right: auto;">
<caption>(\#tab:datapackages)Selected R packages for geographic data retrieval.</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Package </th>
   <th style="text-align:left;"> Description </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> getlandsat </td>
   <td style="text-align:left;"> Provides access to Landsat 8 data. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> osmdata </td>
   <td style="text-align:left;"> Download and import of OpenStreetMap data. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> raster </td>
   <td style="text-align:left;"> getData() imports administrative, elevation, WorldClim data. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> rnaturalearth </td>
   <td style="text-align:left;"> Access to Natural Earth vector and raster data. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> rnoaa </td>
   <td style="text-align:left;"> Imports National Oceanic and Atmospheric Administration (NOAA) climate data. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> rWBclimate </td>
   <td style="text-align:left;"> Access World Bank climate data. </td>
  </tr>
</tbody>
</table>

It should be emphasised that Table \@ref(tab:datapackages) represents only a small number of available geographic data packages.
Other notable packages include **GSODR**, which provides Global Summary Daily Weather Data in R (see the package's [README](https://github.com/ropensci/GSODR) for an overview of weather data sources);
**tidycensus** and **tigris**, which provide socio-demographic vector data for the USA; and **hddtools**, which provides access to a range of hydrological datasets.

Each data package has its own syntax for accessing data.
This diversity is demonstrated in the subsequent code chunks, which show how to get data using three packages from Table \@ref(tab:datapackages).
Country borders are often useful and these can be accessed with the `ne_countries()` function from the **rnaturalearth** package as follows:


```r
library(rnaturalearth)
usa = ne_countries(country = "United States of America") # United States borders
class(usa)
#> [1] "SpatialPolygonsDataFrame"
#> attr(,"package")
#> [1] "sp"
# alternative way of accessing the data, with raster::getData()
# getData("GADM", country = "USA", level = 0)
```

By default **rnaturalearth** returns objects of class `Spatial`.
The result can be converted into an `sf` objects with `st_as_sf()` as follows:


```r
usa_sf = st_as_sf(usa)
```

A second example downloads a series of rasters containing global monthly precipitation sums with spatial resolution of ten minutes.
The result is a multilayer object of class `RasterStack`.










































































