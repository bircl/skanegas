# skanegas
Gas stations in Skane and prices. Webpage to publish spatial and attribute data through WMS, WMTS stored in GeoServer.

### Aim
The design and purpose of this website are to display all available gas stations near Skåane and their corresponding fuel prices through a web map service. This allows users to easily select nearby gas stations with lower fuel prices and view the route to the destination gas station from the map.

### Data

Vector and raster data projected to SWEREF99(EPSG:3006) reference system and it is stored in GeoServer that was built in Nateko department at Lund University. To display each gas station on the web map, the styling of each layer is set by the SLD file in Geoserver. The web map service is built based on OpenLayers3.

#### Existing Sources
Gas Station data was scraped online by using python library selenium and beautifulsoup. Gas stations are provided online in a list where it can be filtered by region and fuel type, and when a gas station is clicked, prices of several fuel types can be displayed.

#### What's New
In our website, we present 179 gas stations, which contain brand, address, phone number, prices for four different fuel type: 95 octanes, 98 octanes, diesel. Since we have 12 different brands, this difference is presented by their brand logos. The road network layer is downloaded from “https://lastkajen.trafikverket.se/”, the original data includes 10 levels of roads in Skåne. In order to have an explicit presentation of gas stations, only six levels are displayed in this web map.

![Gas_stations](/ss/gas_stations.png)

For the heatmap of fuel price, prices are interpolated by IDW and it is clipped within the boundary of Skane region with a cell size of 479m to 479m. Then, on our website, it was rendered by the white-red color scale(Figure 2). The area with the higher price of fuel is shown by darker red with 50% transparency which could also present the gas station at the same time.

![heatmap_diesel](/ss/heatmap_diesel.png)
![heatmap_gas95](/ss/heatmap_gas95.png)

###### CSS

In terms of web map layout, flexbox CSS displaying method is used due to it’s flexible, responsive aspect.

### Functions

The following Openlayers3 functions are utilized: Zoom in/ out, zoom to extent, zoom slider, overview map, scale line, full-screen button, coordinate pair of the cursor. Moreover, to provide a popup menu to users we utilized openlayers3 overlay function and jquery library to fetch feature info of gas stations from GeoServer. This popup menu can be viewed only when the gas station is clicked. This menu is created by two elements: an exit button to close the menu, a container showing the attributes of the station.

Right-top side of the map a checkbox button maintains the transition between three layers: gas stations, road network and interpolated prices. In addition, a dropdown menu located below checkboxes is used to provide a transition between two heatmaps: 95 octanes, diesel.

Besides the functions that bind the map, there are also other functionalities binding the HTML page. Right-bottom of the map, a legend button binds the visibility of legends for the brand of a gas station and interpolated data. Top-right of the webpage, a switch button binds the color of the background and the text to provide a darker display in order to increased user experience in low light condition.

![main_page](/ss/main_page.png)
