# Mapping_Earthquakes

Overview of Project Basil and Sadhana like how you created your earthquake map with two different maps and the earthquake overlay. Now, Basil and Sadhana would like to see the earthquake data in relation to the tectonic plates’ location on the earth, and they would like to see all the earthquakes with a magnitude greater than 4.5 on the map, and they would like to see the data on a third map.

Deliverable 1: Add Tectonic Plate Data Deliverable 2: Add Major Earthquake Data Deliverable 3: Add an Additional Map Deliverable 4: A written report on the Mapping Earthquakes analysis README.md. Resources and Before Start Notes: Data Source: tectonic_plate_starter_logic.js, tectonic_plate_starter_logic.js, tectonic_plate_starter_logic.js and index.html Data Tools: JavaScript, JSON, GeoJSON and IO (Web Server) Software: 

ES6+, ECMAScript and Visual Studio Code 1.50.0 For more information, visit The Mapbox API.

Tech-Overview In this module, you will use the Leaflet.js Application Programming Interface (API) to populate a geographical map with GeoJSON earthquake data from a URL. Each earthquake will be visually represented by a circle and color, where a higher magnitude will have a larger diameter and will be darker in color. In addition, each earthquake will have a popup marker that, when clicked, will show the magnitude of the earthquake and the location of the earthquake.

Basic Project Plan Purpose The purpose of this project is to visually show the differences between the magnitudes of earthquakes all over the world for the last seven days.

Tasks To complete this project, use a URL for GeoJSON earthquake data from the USGS website and retrieve geographical coordinates and the magnitudes of earthquakes for the last seven days. Then add the data to a map.

Approach Your approach will be to use the JavaScript and the D3.js library to retrieve the coordinates and magnitudes of the earthquakes from the GeoJSON data. You'll use the Leaflet library to plot the data on a Mapbox map through an API request and create interactivity for the earthquake data.

Now that you have an overview of the project plan, let's set up a Mapbox account and get the API token you'll need to create geographical maps.

The Leaflet JavaScript Library On the Leaflet homepage, scroll midpage and click the Leaflet Quick Start Guide link:

name-of-you-image

The Leaflet Quick Start Guide provides steps for setting up a Leaflet map. To begin, scroll midpage to the "Preparing your page" section:

name-of-you-image

The "Preparing your page" section includes links and HTML code that we'll add to our Mapping Earthquakes - index.html page.

Use the Leaflet Documentation The Leaflet Quick Start Guide provides the tileLayer() code:

name-of-you-image

We can copy this tile layer code and assign it to the streets variable, since the tile layer will create a street-level map. Add the following code block to your logic.js file:

// We create the tile layer that will be the background of our map. let streets = L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}', { attribution: 'Map data © OpenStreetMap contributors, CC-BY-SA, Imagery (c) Mapbox', maxZoom: 18, id: 'mapbox.streets', accessToken: API_KEY }); // Then we add our 'graymap' tile layer to the map. streets.addTo(map); Let's move on!

Deliverable 1: Add Tectonic Plate Data Deliverable Requirements: Using your knowledge of JavaScript, Leaflet.js, and geoJSON data, you’ll add tectonic plate data using d3.json(), add the data using the geoJSON() layer, set the tectonic plate LineString data to stand out on the map, and add the tectonic plate data to the overlay object with the earthquake data.

Your final map should look similar to the following image:

name-of-you-image

The tectonic plate data is added as a second layer group. The tectonic plate data is added to the overlay object. The d3.json() callback is working and does the following: The tectonic plate data is passed to the geoJSON() layer The geoJSON() layer adds color and width to the tectonic plate lines The tectonic layer group variable is added to the map The earthquake data and tectonic plate data displayed on the map when the page loads. Results with detail analysis: The tectonic plate data is added as a second layer group. Image with JavaScript & HTML Code below.

Code and Image

// 1. Add a 2nd layer group for the tectonic plate data. let allEarthquakes = new L.LayerGroup(); let tectonicPlates = new L.LayerGroup(); name-of-you-image

The tectonic plate data is added to the overlay object. Image with JavaScript & HTML Code below.

Code and Image

// 2. Add a reference to the tectonic plates group to the overlays object. let overlays = { "Earthquakes": allEarthquakes, "Tectonic Plates": tectonicPlates,

};

// Then we add a control to the map that will allow the user to change which // layers are visible. L.control.layers(baseMaps, overlays).addTo(map);

// Retrieve the earthquake GeoJSON data. d3.json("https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson").then(function(data) {

// This function returns the style data for each of the earthquakes we plot on // the map. We pass the magnitude of the earthquake into two separate functions // to calculate the color and radius. function styleInfo(feature) { return { opacity: 1, fillOpacity: 1, fillColor: getColor(feature.properties.mag), color: "#000000", radius: getRadius(feature.properties.mag), stroke: true, weight: 0.5 }; }

// This function determines the color of the marker based on the magnitude of the earthquake. function getColor(magnitude) { if (magnitude > 5) { return "#ea2c2c"; } if (magnitude > 4) { return "#ea822c"; } if (magnitude > 3) { return "#ee9c00"; } if (magnitude > 2) { return "#eecc00"; } if (magnitude > 1) { return "#d4ee00"; } return "#98ee00"; } name-of-you-image

The d3.json() callback is working and does the following: The tectonic plate data is passed to the geoJSON() layer The geoJSON() layer adds color and width to the tectonic plate lines The tectonic layer group variable is added to the map Image with JavaScript & HTML Code below.

// 3. Use d3.json to make a call to get our Tectonic Plate geoJSON data. d3.json("https://raw.githubusercontent.com/fraxen/tectonicplates/master/GeoJSON/PB2002_boundaries.json").then(function(plateData) { // Adding our geoJSON data, along with style information, to the tectonicplates // layer. L.geoJson(plateData, { color: "#ff6500", weight: 2 }) .addTo(tectonicPlates); name-of-you-image

The earthquake data and tectonic plate data displayed on the map when the page loads. Image with JavaScript & HTML Code below.

Code and Image

// COLUMBIA ENGINEERING // By Emmanuel Martinez // Module 13

  // Then add the tectonicplates layer to the map.
  tectonicPlates.addTo(map);
name-of-you-image

Deliverable 2: Add Major Earthquake Data Deliverable Requirements: Using your knowledge of JavaScript, Leaflet.js, and geoJSON data, you’ll add major earthquake data to the map using d3.json(), and a color and set the radius of the circle based on the magnitude of earthquake, and add a popup marker for each earthquake that displays the magnitude and location of the earthquake using the GeoJSON layer, geoJSON().



The major earthquake data is added as a third layer group. The major earthquake data is added to the overlay object. The d3.json() callback is working and does the following: Sets the color and diameter of each earthquake. The major earthquake data is passed to the geoJSON() layer. The geoJSON() layer creates a circle for each major earthquake, and adds a popup for each circle to display the magnitude and location of the earthquake The major earthquake layer group variable is added to the map All the earthquake data and tectonic plate data are displayed on the map when the page loads and the datasets can be toggled on or off. Results with detail analysis: The major earthquake data is added as a third layer group. Image with JavaScript & HTML Code below.

Code and Image

// DELIVERABLE 2 

// 1. Add a 3rd layer group for the tectonic plate data. let allEarthquakes = new L.LayerGroup(); let tectonicPlates = new L.LayerGroup(); let majorEarthquakes = new L.LayerGroup(); name-of-you-image

The major earthquake data is added to the overlay object. Image with JavaScript & HTML Code below.

Code and Image

// DELIVERABLE 2 

// 2. Add a reference to the tectonic plates group to the overlays object. let overlays = { "Earthquakes": allEarthquakes, "Tectonic Plates": tectonicPlates, "Major Earthquakes": majorEarthquakes }; name-of-you-image

The d3.json() callback is working and does the following: Sets the color and diameter of each earthquake. The major earthquake data is passed to the geoJSON() layer. The geoJSON() layer creates a circle for each major earthquake, and adds a popup for each circle to display the magnitude and location of the earthquake The major earthquake layer group variable is added to the map Image with JavaScript & HTML Code below.

Code and Image

// DELIVERABLE 2 

// 3. Retrieve the major earthquake GeoJSON data >4.5 mag for the week. d3.json("https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/4.5_week.geojson").then(function(data) {

// 4. Use the same style as the earthquake data. function styleInfo(feature) { return { opacity: 1, fillOpacity: 1, fillColor: getColor(feature.properties.mag), color: "#000000", radius: getRadius(feature.properties.mag), stroke: true, weight: 0.5 }; }

// 5. Change the color function to use three colors for the major earthquakes based on the magnitude of the earthquake. function getColor(magnitude) { if (magnitude > 5) { return "#ea2c2c"; } if (magnitude > 4) { return "#ea822c"; } return "#eecc00"; }

// 6. Use the function that determines the radius of the earthquake marker based on its magnitude. function getRadius(magnitude) { if (magnitude === 0) { return 1; } return magnitude * 4; }

// 7. Creating a GeoJSON layer with the retrieved data that adds a circle to the map // sets the style of the circle, and displays the magnitude and location of the earthquake // after the marker has been created and styled. L.geoJson(data, { // We turn each feature into a circleMarker on the map. pointToLayer: function(feature, latlng) { console.log(data); return L.circleMarker(latlng); }, // We set the style for each circleMarker using our styleInfo function. style: styleInfo, // We create a popup for each circleMarker to display the magnitude and location of the earthquake // after the marker has been created and styled. onEachFeature: function(feature, layer) { layer.bindPopup("Magnitude: " + feature.properties.mag + "
Location: " + feature.properties.place); } }).addTo(majorEarthquakes);

// 8. Add the major earthquakes layer to the map. majorEarthquakes.addTo(map);

// 9. Close the braces and parentheses for the major earthquake data. }); name-of-you-image

All the earthquake data and tectonic plate data are displayed on the map when the page loads and the datasets can be toggled on or off. Image with JavaScript & HTML Code below.

Code and Image

d3.json("https://raw.githubusercontent.com/fraxen/tectonicplates/master/GeoJSON/PB2002_boundaries.json").then(function(plateData) { // Adding our geoJSON data, along with style information, to the tectonicplates // layer. L.geoJson(plateData, { color: "#ff6500", weight: 2 }) .addTo(tectonicPlates);

  // Then add the tectonicplates layer to the map.
  tectonicPlates.addTo(map);
}); }); name-of-you-image

Deliverable 3: Add an Additional Map Deliverable Requirements: Using your knowledge of JavaScript and Leaflet.js add a third map style to your earthquake map.

Your final map should look similar to the following image:

name-of-you-image

A third map tile layer is created. The third map is added to the overlay object. All the earthquake data and tectonic plate data are displayed on the all maps of the webpage. Results with detail analysis: A third map tile layer is created. Image with JavaScript & HTML Code below.

Code and Image

// DELIVERABLE 3 

// We create a third tile layer that will be the background of our map. let dark = L.tileLayer('https://api.mapbox.com/styles/v1/mapbox/dark-v10/tiles/{z}/{x}/{y}?access_token={accessToken}', { attribution: 'Map data © OpenStreetMap contributors, CC-BY-SA, Imagery (c) Mapbox', maxZoom: 18, accessToken: API_KEY }); name-of-you-image

The third map is added to the overlay object. Image with JavaScript & HTML Code below.

Code and Image

// DELIVERABLE 3 

// Create a base layer that holds all three maps. let baseMaps = { "Streets": streets, "Satellite": satelliteStreets, "Dark": dark }; name-of-you-image

All the earthquake data and tectonic plate data are displayed on the all maps of the webpage. Image with JavaScript & HTML Code below.



// 9. Create the layout for the bar chart. 
var barLayout = {
 title: "Top 10 Bacteria Cultures Found"
};
// 10. Use Plotly to plot the data with the layout. 
Plotly.newPlot("bar", barData, barLayout);
