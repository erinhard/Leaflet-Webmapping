NY County Webmap HTML Code

# View map [here](https://erinhard.github.io/NY-State-County-Map/)

<!DOCTYPE html>
<html>
<head>

	<title>NY Counties</title>

	<meta charset="utf-8" />
	<meta name="viewport" content="width=device-width, initial-scale=1.0">

	<link rel="shortcut icon" type="image/x-icon" href="docs/images/favicon.ico" />

    	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css" integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ==" crossorigin=""/>
   	<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js" integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og==" crossorigin=""> </script>
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
	.legend { text-align: left; line-height: 18px; color: #555; } .legend i { width: 18px; height: 18px; float: left; 	margin-right: 8px; opacity: 0.7; }</style>
	
	</head>
	<body>

	<div id='map'></div>

	<script type="text/javascript">

	var map = L.map('map').setView([43.015480, -76.088416], 7);

	//Adding a topographic basemap and a grayscale basemap from Mapbox:// 

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

	//Add geojson object and add color:// 

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

	//Overlaying with a popup and info on hover for my geojson object://

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

**Get basemaps** [here](https://leaflet-extras.github.io/leaflet-providers/preview/)

Markdown features:
- Bulleted
- List
1. Numbered
2. List
**Bold** and _Italic_ and `Code` text
[Link](url) and ![Image](src)
