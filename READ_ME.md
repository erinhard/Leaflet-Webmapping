---
title: "READ_ME"
output: html_document
---

library(rgdal)
library(leaflet)

industry <- read.csv("C:/Users/ER023HA/Documents/boundaries/soils/tri_2018_nh.csv", stringsAsFactors = FALSE)

nh <- rgdal::readOGR("C:/Users/ER023HA/Documents/boundaries/soils/new_hampshire.geojson")

pal <- colorFactor(c("green", "red"), domain = c("NO", "YES"))

leaflet() %>%
  addProviderTiles(providers$Esri.WorldStreetMap, group = "Street") %>%
  addProviderTiles(providers$Esri.WorldImagery, group = "Satellite") %>%
  addPolygons(data = nh, smoothFactor = 0.5, weight = 2, opacity = 1, fillOpacity = 0, dashArray = "3", color = "white") %>%
  addCircleMarkers(data = industry, industry$LONGITUDE, industry$LATITUDE, opacity = 1, fillOpacity = 1, color = ~pal(industry$CARCINOGEN),  
                   popup = paste(industry$FACILITY.NAME, "<br>", 
                                 "<strong>Chemicals Released: </strong>", industry$CHEMICAL, "<br>", 
                                 "Industrial Sector: ", industry$INDUSTRY.SECTOR, "<br>", 
                                 "Activity or Production? ", industry$PROD_RATIO_OR_.ACTIVITY, "<br>", 
                                 "<strong>Is this chemical a Carcinogen? </strong>", industry$CARCINOGEN, "<br>", 
                                 "Is this chemical a metal? ", industry$METAL), 
                   label = ~industry$FACILITY.NAME, 
                   labelOptions = labelOptions(style = list("font-style" = "bold", "font-size" = "13px"))) %>% 
  addLegend("topright", pal = pal, values = industry$CARCINOGEN, 
            title = "2018 New Hampshire Toxics Release Inventory (TRI)<br><br>A qualitative interactive map showing specific toxins released from industrial companies<br><br>https://catalog.data.gov/dataset/toxic-release-inventory-tri-8162e<br><br>Does the EPA classify this chemical as a carcinogen?", 
            opacity = 0.6) %>%
  addLayersControl(baseGroups = c("Street", "Satellite"))
