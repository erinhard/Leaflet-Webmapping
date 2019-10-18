NY State County Webmap

You can use the [editor on GitHub](https://github.com/erinhard/pleasant-programming-partner/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

# Starting out:

<!DOCTYPE html>
<html>
<head>

	<title>NY State Counties</title>

	<meta charset="utf-8" />
	<meta name="viewport" content="width=device-width, initial-scale=1.0">

	<link rel="shortcut icon" type="image/x-icon" href="docs/images/favicon.ico" />

    	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css" integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ==" crossorigin=""/>
   	<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js" integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og==" crossorigin=""></script>

<style>
html, body {
	height: 100%;
	margin: 0;
}
	
#map {
	width: 600px;
	height: 400px;
}
</style>

<style>#map { width: 100%; height: 100%; }
.info { padding: 6px 8px; font: 14px/16px Arial, Helvetica, sans-serif; background: white; background: rgba(255,255,255,0.8); box-shadow: 0 0 15px rgba(0,0,0,0.2); border-radius: 5px; } .info h4 { margin: 0 0 5px; color: #777; }
.legend { text-align: left; line-height: 18px; color: #555; } .legend i { width: 18px; height: 18px; float: left; margin-right: 8px; opacity: 0.7; }</style>
	
</head>
<body>

<div id='map'></div>

<script type="text/javascript">

var map = L.map('map').setView([43.015480, -76.088416], 7);

**Get basemaps** [here](https://leaflet-extras.github.io/leaflet-providers/preview/)

# Adding a topographic basemap and a grayscale basemap from Mapbox: 

var OpenTopoMap = L.tileLayer('https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', {
	maxZoom: 17,
	attribution: 'Map data: &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, <a href="http://viewfinderpanoramas.org">SRTM</a> | Map style: &copy; <a href="https://opentopomap.org">OpenTopoMap</a> (<a href="https://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA</a>)'
}).addTo(map);

var Grayscale = L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
	maxZoom: 18,
	attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
		'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
		'Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
	id: 'mapbox.light'
}).addTo(map);

# Add geojson object and add color: 

var county = {
"type": "FeatureCollection",
"name": "ny_county",
"crs": { "type": "name", "properties": { "name": "urn:ogc:def:crs:EPSG::4269" } },
"features": [=]
};

var countyStyle = {
	"color": "#de2d26",
	"weight": 3,
	"opacity": 1,
	"fillOpacity": 0
};

# Overlaying with a popup and info on hover for my geojson object:

var baseMaps = {
	"Topographic": OpenTopoMap,
	"Grayscale": Grayscale
};

var overlayMaps = {
"Counties": L.geoJSON(county, {
	style: countyStyle,
	onEachFeature: function(feature, layer) {
		layer.bindPopup('<h1>'+feature.properties.NAMELSAD+'</h1>'),
		layer.bindTooltip(feature.properties.NAMELSAD)
	}
})
};

L.control.layers(baseMaps, overlayMaps).addTo(map);

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/erinhard/pleasant-programming-partner/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
