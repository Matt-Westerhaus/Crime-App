<script>
import $ from 'jquery'
export default {
    data() {
        return {
            location: '',
            view: 'map',
            codes: [],
            neighborhoods: [],
            incidents: [],
            leaflet: {
                map: null,
                center: {
                    lat: 44.955139,
                    lng: -93.102222,
                    address: ""
                },
                zoom: 12,
                bounds: {
                    nw: {lat: 45.008206, lng: -93.217977},
                    se: {lat: 44.883658, lng: -92.993787}
                },
                neighborhood_markers: [
                    {location: [44.942068, -93.020521], marker: null},
                    {location: [44.977413, -93.025156], marker: null},
                    {location: [44.931244, -93.079578], marker: null},
                    {location: [44.956192, -93.060189], marker: null},
                    {location: [44.978883, -93.068163], marker: null},
                    {location: [44.975766, -93.113887], marker: null},
                    {location: [44.959639, -93.121271], marker: null},
                    {location: [44.947700, -93.128505], marker: null},
                    {location: [44.930276, -93.119911], marker: null},
                    {location: [44.982752, -93.147910], marker: null},
                    {location: [44.963631, -93.167548], marker: null},
                    {location: [44.973971, -93.197965], marker: null},
                    {location: [44.949043, -93.178261], marker: null},
                    {location: [44.934848, -93.176736], marker: null},
                    {location: [44.913106, -93.170779], marker: null},
                    {location: [44.937705, -93.136997], marker: null},
                    {location: [44.949203, -93.093739], marker: null}
                ]
            }
        };
    },
    methods: {
        drawMarker() {
          let i = 0;
          for (i; i < this.leaflet.neighborhood_markers.length; i++) {
            // Set temp marker to have neighbor coordinate
            let temp_marker = new L.Marker([this.leaflet.neighborhood_markers[i].location[0], this.leaflet.neighborhood_markers[i].location[1]]);
            // Set neighbor marker to be temp marker
            this.leaflet.neighborhood_markers[i].marker = temp_marker;
            // Add marker to map
            temp_marker.addTo(this.leaflet.map);
          }  
        },
        // TODO: If they search wit lat/lon instead of a street/place name
        searchLocation() {
            let url = "https://nominatim.openstreetmap.org/?street='"
            url += this.location + "'&format=json&limit=1";
            this.getJSON(url)
            .then((data) => {
                // Clamp coordinate if lat or lon is out of bbound
                if (data[0].lat < 44.883658) {
                    data[0].lat = 44.883658;
                } 
                if (data[0].lat < -93.217977) {
                    data[0].lat = -93.217977;
                }
                if (data[0].lon > 45.008206) {
                    data[0].lon = 45.008206;
                }
                if (data[0].lon > -92.993787) {
                    data[0].lon = -92.993787;
                }
                // Zoom to search location
                this.leaflet.map.flyTo(new L.LatLng(data[0].lat, data[0].lon), 18);    
                // Creating a marker
                let marker = new L.Marker([data[0].lat, data[0].lon]);
                // Adding marker to the map
                marker.addTo(this.leaflet.map);
            })
            .catch((err) => {
            });
        },
        viewMap(event) {
            this.view = 'map';
        },
        viewNewIncident(event) {
            this.view = 'new_incident';
        },
        viewAbout(event) {
            this.view = 'about';
        },
        getJSON(url) {
            return new Promise((resolve, reject) => {
                $.ajax({
                    dataType: 'json',
                    url: url,
                    success: (response) => {
                        resolve(response);
                    },
                    error: (status, message) => {
                        reject({status: status.status, message: status.statusText});
                    }
                });
            });
        },
        uploadJSON(method, url, data) {
            return new Promise((resolve, reject) => {
                $.ajax({
                    type: method,
                    url: url,
                    contentType: 'application/json; charset=utf-8',
                    data: JSON.stringify(data),
                    dataType: 'text',
                    success: (response) => {
                        resolve(response);
                    },
                    error: (status, message) => {
                        reject({status: status.status, message: status.statusText});
                    }
                });
            });
        }
    },
    mounted() {
        this.leaflet.map = L.map('leafletmap').setView([this.leaflet.center.lat, this.leaflet.center.lng], this.leaflet.zoom);
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
            minZoom: 11,
            maxZoom: 18
        }).addTo(this.leaflet.map);
        this.leaflet.map.setMaxBounds([[44.883658, -93.217977], [45.008206, -92.993787]]);
        let district_boundary = new L.geoJson();
        district_boundary.addTo(this.leaflet.map);
        this.getJSON('/data/StPaulDistrictCouncil.geojson').then((result) => {
            // St. Paul GeoJSON
            $(result.features).each((key, value) => {
                district_boundary.addData(value);
            });
        }).catch((error) => {
            console.log('Error:', error);
        });
    },
}
</script>

<template>
    <div class="grid-container">
        <div class="grid-x grid-padding-x">
            <p :class="'cell small-4 ' + ((view === 'map') ? 'selected' : 'unselected')" @click="viewMap">Map</p>
            <p :class="'cell small-4 ' + ((view === 'new_incident') ? 'selected' : 'unselected')" @click="viewNewIncident">New Incident</p>
            <p :class="'cell small-4 ' + ((view === 'about') ? 'selected' : 'unselected')" @click="viewAbout">About</p>
        </div>
    </div>
    <div v-show="view === 'map'">
        <div class="grid-container">
            <div class="grid-x grid-padding-x">
                <div style = "position:absolute; left:80px; top:20px;">
                    <!--Input TextBox-->
                    <input class="e-input" type="text" v-model="location" placeholder="Enter Location or Coord." />
                    <button type="button" class="button" @click="searchLocation">Go</button>
                </div>
                <div id="leafletmap" class="cell auto"></div>
                <div>
                    <table style="position:relative; left:1em;">
                        <thead>
                            <tr>
                            <th width="100">Neighborhood Name</th>
                            <th width="100">Incident Type</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                            <td>TBD</td>
                            <td>TBD</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
    <div v-if="view === 'new_incident'">
        <!-- Replace this with your actual form: can be done here or by making a new component -->
        <div class="grid-container">
            <div class="grid-x grid-padding-x">
                <h1 class="cell auto">New Incident Form</h1>
                <form>
                    <label for="case_number">Case Number:</label><br>
                    <input type="text" id="case_numver"><br>
                    <label for="date_time">Date & Time:</label><br>
                    <input type="datetime-local" id="date_time"><br>
                    <label for="code">Code:</label><br>
                    <input type="number" id="code"><br>
                    <label for="incident">Incident:</label><br>
                    <input type="text" id="code"><br>
                    <label for="police_grid">Police Grid:</label><br>
                    <input type="number" id="police_grid"><br>
                    <label for="neighborhood_number">Neighborhood Number:</label><br>
                    <input type="number" id="neighborhood_number"><br>
                    <label for="block">Block:</label><br>
                    <input type="text" id="block"><br>

                    <button type="button">Submit</button>

                </form>
            </div>
        </div>
    </div>
    <div v-if="view === 'about'">
        <!-- Replace this with your actual about the project content: can be done here or by making a new component -->
        <div class="grid-container">
            <div class="grid-x grid-padding-x">
                <h1 class="cell auto">About the Project</h1>
            </div>
        </div>
    </div>
</template>

<style>
#leafletmap {
    height: 500px;
}
.selected {
    background-color: rgb(10, 100, 126);
    color: white;
    border: solid 1px white;
    text-align: center;
    cursor: pointer;
}
.unselected {
    background-color: rgb(200, 200, 200);
    color: black;
    border: solid 1px white;
    text-align: center;
    cursor: pointer;
}
</style>

