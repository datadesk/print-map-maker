Print map maker
===============

A tool to generate print maps from Mapbox tiles

Simple print locator maps are extremely effective storytelling tools, but they can take a long time to produce. Why? Well, to start with, you have to find a reference that is licensed to use, digitize it and redraw the information, which can be a lot of work for an element that is 2 inches square.

GIS is a solid step in the right direction. And for larger maps, especially those that illustrate complex data, it’s the tool of choice. But that’s a specialized skill that doesn’t exist on every staff.

Print Map Maker allows artists and designers to create quality maps at a resolution high enough to look crisp on newsprint. We’ve been experimenting and publishing with this tool for six months and it has served us remarkably well.

* * *

![Print map maker in action.](img/print-map-maker-example.gif)

### How it's done

Print Map Maker pulls in a global map generated from custom vector tiles created in [Mapbox Studio](https://www.mapbox.com/mapbox-studio/) using [OpenStreetMap](http://www.openstreetmap.org/) data and displays them using Mapbox's version of [leaflet.js](http://leafletjs.com/). 

[Geocodify](https://github.com/datadesk/jquery-geocodify) is used to autocomplete the address field and Mapbox's geocoder re-centers the map to the location. These can be adjusted or eliminated based on your needs. 

An image is generated using the [leaflet-image](https://github.com/mapbox/leaflet-image) plugin and appears at the bottom of your page. Download the image and resize it an image editing program.   


### Getting started

Clone the repo to your computer. You can either download it as a ZIP file or use the command line.

Swap "YOUR API KEY" in the index.html file with your Deafult Public Token from Mapbox. You can find it here (https://www.mapbox.com/account/apps/) when you set up an account. Then replace it here:

    L.mapbox.accessToken = 'YOUR API KEY';

Next you will need a map layer. Download and open [Mapbox Studio](https://www.mapbox.com/mapbox-studio/) and create a new [style](https://www.mapbox.com/mapbox-studio/style-quickstart/). You don't need to customize yet. Just make a new style, save it and upload it. Mapbox studio will generate a style name that looks similar to this: "yourusername.f3da9821" Replace it here:

	<option value="latimesmapping.f3da9821">
		Flat World
	</option>

When you edit your style and re-upload, the changes will overwrite so your style should still work. Each map style you create can be added as an additional option.

Open the index.html file in a browser and you're ready to test.


### Sizing: Multiples of three

If you plan to use this for print newspaper production, it helps to think of everything in multiples of three.

Assuming you have standard column sizes, you need to figure out the pixel width of your columns. If you use Adobe Illustrator, open your document and change the Units preferences to pixels. If your one-column graphic is 100 pixels wide, make your one-column div in the HTML page 300px (three times the width).

Here's where you change the sizes in the index.html page

    <style type="text/css" media="screen">

    #map_1col{width:330px; height:700px;}
    #map_2col{width:699px; height:1200px;}
    #map_3col{width:1065px; height:1200px;}
    #map_4col{width:1434px; height:1200px;}
    #map_web{width:1300px; height:731px;}

The tool generates a 72-ppi image, which translates to 72 dpi for print folk. When the oversized image is downloaded it can be resized (without resampling) from a 72-ppi image to 216 ppi (3x) in Photoshop. Save the resulting image and it should fit perfectly in your document where labels can be added.

### Customizing map tiles

Customizing map features works the same way. If your streets are 1 point wide, make them 3 points wide in Mapbox Studio and they will scale back down in the final image. The streets in the example below end up 0.65 points wide. You can adjust the appearance at each zoom level.

    [class='street']{
      [zoom>=0] { line-width: 0; }
      [zoom>=12] { line-width: 0.6; }
      [zoom>=13] { line-width: 1; }
      [zoom>=14] { line-width: 1.95; }
      [zoom>=15] { line-width: 1.95; }
      [zoom>=16] { line-width: 1.95; }
    }

Custom map styles require a subscription to Mabox. A free subscription will get you one style. Five dollars per month will get you three and $49 per month will get you 10. That may seem like a lot but it's worth it considering for the production time saved. 

A simplified set of styles is included. Open the Styles folder and then open mapbox-studio-style in a text editor. These are the map styles written in CartoCSS, which is similar to the styling used in HTML pages. 

In Mapbox Studio, create a new project based on OSM bright and take note of the style sheet on the left. Copy and paste the styles from the open document and replace the styles in Mapbox Studio. Save the project and you are ready to start customizing to match your styles. Experiment. You can always re-paste the original if something gets broken.

### The GeoJSON layer
![Example image with GeoJSON boundaries added](img/print-map-maker-example-2.gif)

<br/>*Downtown Los Angeles with GeoJSON boundaries added.*

To add boundary, line or point layers, paste the properly formatted GeoJSON into the field and click to ADD GeoJSON. It automatically applies styles for polygons, lines and points and adds them to all the maps. You can add multiple layers. If you are new to GeoJson learn more at [Wikipedia](http://en.wikipedia.org/wiki/GeoJSON), read the [specification](http://geojson.org/geojson-spec.html) or generate your own at [geojson.io](http://geojson.io/#map=2/20.0/0.0).


### Licensing
Mapbox and OpenStreetMap [license](http://www.openstreetmap.org/copyright) their data/tools. Print map maker strips the credit when the image is generated so a credit must be added below a map when publishing as seen in the photograph of a printed map below. 

![Photograph of a printed map made with the tool.](img/example2.jpg)
 