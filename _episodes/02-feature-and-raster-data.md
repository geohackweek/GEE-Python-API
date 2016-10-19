---
title: "Feature & Raster Data"
teaching: 45
exercises: 15
questions:
- "What is the difference between feature and raster data in Earth Engine?"
- "How do I load, visualize and filter feature and image data in GEE?"
objectives:
- "Load datasets and successfully visualize in the GEE API"
- "Filter an image collection"
- "Know how to share code and manage versions"

keypoints:
- Visualizing images in the Javascript API can take some guesswork; use the Inspector to help. 
--- Feature data is cast as vector data and rasters are cast as images in GEE. 
--- Use the assets manager, your google drive and shpEscape to get images and vector data in and out of Google Earth Engine and to share code.
 

## Features, Images and Collections 

#### Features & Images
* Feature data includes all vector data with geometry such as points, lines and polygons (like shapefiles) such as a watershed outline.

* Images are rasters. They can have more than one band and each band has its own data type, name, resolution, and metadata. 
* An example image might be a GlobCover raster of land use/land cover where  each pixel has a number that represents its land cover classification. 

##### Collections
 
Often we are not working with a single image or feature. 

* An image collection is a multidimensional stack or time series of images.  
    * Landsat, MODIS, Sentinel satellite imagery
    * a digital elevation model
    * gridded population estimates
    * global land cover maps
* A feature collection is a collection of features. 
	* an outline of a watershed
	* sampling point from a field study
	* a table of annual glacial maximums associated with a lat/long

For each of these data types, there are vast quantities of data already available in GEE or you can import or create your own features, images and collections. 


### Loading, Visualizing, Clipping and Filtering

#### Loading Features

Let's load an existing Feature Collection of watershed outlines.  

	var watersheds = ee.FeatureCollection("ft:1IXfrLpTHX4dtdj1LcNXjJADBB-d93rkdJ9acSEWK")
	Map.addLayer(watersheds, null, 'watersheds')

A map will appear that should look like this: 

![optional caption text](watersheds.png)


You can go down to the mapping window and play with the zoom, the background and the transparency.

#### Filtering Feature Collections 

We only care about Seattle, so we want to isolate our watershed name. To do this, click on the "Inspector" tab up on the right next to the Console. Then, scroll over to Seattle, click on the map and see what pops up in the "Inspector" window. What is the name of the HUC 6 that Seattle is located in?

In order to filter the feature collection down to just that region, use the following:
	
	var pugetSound= watersheds.filter(ee.Filter.contains('name', 'Puget Sound'));
	Map.addLayer(pugetSound, null, 'Puget Sound')   

#### Loading and Visualizing an Image

Let's load a couple different interesting images into our window.
	
	var elevation = ee.Image("USGS/NED")
	Map.addLayer(elevation, {min:0, max:3000, palette:['000000',"ffffff"]},"elevation");

#### Clipping the Image 
Whoa. Look at the power! This is a digital elevation model for the whole United States with a resolution of 10 meters! While cool, we only want the elevation in our study area.
	
	Map.addLayer(elevation.clip(pugetSound), {min:0, max:3000, palette:['000000',"ffffff"]},"elevation2");

#### Adjusting visualization parameters
Notice your screen is entirely blank. What do you suspect happened?
You can fix this by adjusting the min and the max. Try this for example:
	
	Map.addLayer(elevation.clip(pugetSound), {min:0, max:300, palette:['000000',"ffffff"]},"elevation2");

*Earth Engine Documentation: https://developers.google.com/earth-engine/image_overview*

### Finding your Way Around (Print is your Friend)

Let's explore this feature collection a little bit. First, type this into your coding console:
	
	print(watersheds)
	print(elevation)

Click around. How many features, or HUC6 watersheds are there? What kind of information or properties does each feature have?
Now try this and notice what changes:
	
	print(watersheds, 'watersheds')

You can do other cool stuff with print, too. 

	// Print the first feature in a collection	
	print(sheds.limit(1)); 

## Image Collections 

Let's use the GRIDMET image collection to find out where the wind was the strongest during Wind-A-Geddon, a large storm that happened this October in Seattle. 

#### Filtering an Image Collection 
GRIDMET is an image collection where each image in the collection represents 1 day of data and each band is a different variable (air temp, precip, etc). 

Where was it the windiest in the Puget Sound Region during Wind-A-Geddon?
	
	var windSpeed = ee.Image(ee.ImageCollection('IDAHO_EPSCOR/GRIDMET').filterDate
		('2016-10-08', '2016-10-12').select("vs").max())  

	Map.addLayer(windSpeed, {min: 2, max: 10, 
		palette: '0157e0,01e013,fafa5a, FF0000'},  'windSpeed')

### Importing Your Own Data

#### Sidenote About Fusion Tables 

* Features Collections are Fusion Tables that exist outside the world of GEE, sort of like a google doc. You can find the link to the Fusion Table in the Metadata.
* Look's go take a look at the watersheds Fusion Table. 
	* [ https://fusiontables.google.com/DataSource?docid=1IXfrLpTHX4dtdj1LcNXjJADBB-d93rkdJ9acSEWK#rows:id=1](https://fusiontables.google.com/DataSource?docid=1IXfrLpTHX4dtdj1LcNXjJADBB-d93rkdJ9acSEWK#rows:id=1)

### Importing
* Upload your own data into Fusion Tables using shpEscape and [the instructions here. ](https://developers.google.com/earth-engine/importing)
* Upload your own Images [using the Asset Manager](https://developers.google.com/earth-engine/asset_manager) in the Code Editor. 

