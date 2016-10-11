---
title: "Introduction to the Google Earth Engine Javascript API"
teaching: 15
exercises: 0
questions:
- "What is the Google Earth Engine Javascript API?"
- "How do I use it?" 
objectives:
- Access the Javascript API, write a script and save it
- Identify helpful elements of the Javascript Code Editor
- Peruse available EE datasets
keypoints:
- GEE's enormous repository of cloud-based imagery allows you do to crazy operations on big datasets from a browser window without having to download anything.
- The Javascript Code Editor is a great way to get started with GEE because it has more robust documentation than the Python API.
- high resolution models and observations are producing gridded datasets that are too large for in-memory processes
- Three useful places to find help are the User Guides, the Forum and the example scripts that come pre-loaded in the repository.

Introduction to Google Earth Engine
---
### Background:

> Google Earth Engine is a cloud-base geoprocessing platform. 
> This platform, built to tackle global environmental challenges, features terabytes of geodata housed in the cloud on which users can performed advanced computation through time and space. Think GLOBAL BIG DATA at your fingertips.

<br>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/27/FP_Satellite_icon.svg/1024px-FP_Satellite_icon.svg.png" width = "200" border = "10">
<br>

### Opening the API:

Use the following link to access the Google Earth Engine Javascript API:

		https://code.earthengine.google.com/

### API Scavenger Hunt:

In the API window, follow along and try to find all of these useful elements. This short tour should help you get oriented to the API. 

1. Where are my scripts and rasters stored?
   * Scripts   
   * Assets   
 
2. Where can I get help when I want to write some code? 
   * Docs (left-hand side) <br>
   * Help > Documentation <br>
   * Help > Users Forum   
 
3. How do I find out what datasets are in Earth Engine or request new ones?
    * Search Toolbar type in *snow* to see how it works
	* GEE Main Website > [Datasets](http://earthengine.google.com/datasets/)
	* Dataset Request   

4.  Where do I type in my code? How do I make it run?

The coding console aka Playground! Try it by typing 
		
		// I love donuts.
		
This is how you write comments. This code won't do anything, it is just there for you to write programmer-readable explanations and annotations. Now go to the top and click "Run". Your code will run -even though it is basically empty.


5.  How do I run, save and share scripts? 

Change the comment to read:
    
		// GeoHack Week Demo Script

 Now click "Save". You can tell when a script hasn't been saved because it will have a * next to the title. Now that you have saved the script, click "Get Link". If you look at your browser, you will see a new unique URL gets generated. You can copy this link and use it to share scripts with anyone else who is a Trusted Tester.


### Cool New Features:

* Profiler
* Revision Histories
* Shortcuts

### Shortcomings and Benefits:

There is an even easier-to-use access point called the Graphical User Interface. It is all just clicking buttons, but has very limited functionality. You could also call into Google using Python, but there isn't so much a developed API for Python (yet). The Python API is very powerful and allows users (perhaps) more knobs to turn, but this API is great if you want to the ease of a developed API combined with the existing robust User Guide and Help Forum, most of which is geared towards JavaScript users. 