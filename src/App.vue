<script>
import $ from 'jquery'
import about from './components/about.vue'
import new_incident from './components/new_incident.vue'
export default {
    data() {
        return {
            textbox: "",
            incidents: "",
            neighborhoods: "",
            codes_json: "",
            location: "",
            view: "map",
            codes: [],
            neighborhoods: [],
            incidents: [],
            crimesCounter: [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
            leaflet: {
                map: null,
                center: {
                    lat: 44.955139,
                    lng: -93.102222,
                    address: ""
                },
                zoom: 12,
                bounds: {
                    nw: { lat: 45.008206, lng: -93.217977 },
                    se: { lat: 44.883658, lng: -92.993787 }
                },
                neighborhood_markers: [
                    { location: [44.942068, -93.020521], marker: null, onMap: true, crimeCount: 2},
                    { location: [44.977413, -93.025156], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.931244, -93.079578], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.956192, -93.060189], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.978883, -93.068163], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.977525, -93.106491], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.959639, -93.121271], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.947700, -93.128505], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.930276, -93.119911], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.982752, -93.14791],  marker: null, onMap: true, crimeCount: 0},
                    { location: [44.963631, -93.167548], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.973971, -93.197965], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.949043, -93.178261], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.934848, -93.176736], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.913106, -93.170779], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.937705, -93.136997], marker: null, onMap: true, crimeCount: 0},
                    { location: [44.949203, -93.093739], marker: null, onMap: true, crimeCount: 0}
                ]
            }
        };
    },
    methods: {
        drawMarker() {
            for (let i = 0; i < this.leaflet.neighborhood_markers.length; i++) {
                // Set temp marker to have neighbor coordinate
                let temp_marker = new L.Marker([this.leaflet.neighborhood_markers[i].location[0], this.leaflet.neighborhood_markers[i].location[1]]);
                temp_marker.bindPopup("The number of crimes commited in this neighborhood is: " + this.leaflet.neighborhood_markers[i].crimeCount);
                // Set neighbor marker to be temp marker
                this.leaflet.neighborhood_markers[i].marker = temp_marker;
                // Add marker to map
                temp_marker.addTo(this.leaflet.map);
            }
        },
        // TODO: If they search wit lat/lon instead of a street/place name
        searchLocation() {
            let url = "https://nominatim.openstreetmap.org/?street='";
            url += this.location + "'&format=json&limit=1";
            this.getJSON(url)
                .then((data) => {
                // Clamp coordinate if lat or lon is out of bound
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
            this.view = "map";
        },
        viewNewIncident(event) {
            this.view = "new_incident";
        },
        viewAbout(event) {
            this.view = "about";
        },
        getJSON(url) {
            return new Promise((resolve, reject) => {
                $.ajax({
                    dataType: "json",
                    url: url,
                    success: (response) => {
                        resolve(response);
                    },
                    error: (status, message) => {
                        reject({ status: status.status, message: status.statusText });
                    }
                });
            });
        },
        uploadJSON(method, url, data) {
            return new Promise((resolve, reject) => {
                $.ajax({
                    type: method,
                    url: url,
                    contentType: "application/json; charset=utf-8",
                    data: JSON.stringify(data),
                    dataType: "text",
                    success: (response) => {
                        resolve(response);
                    },
                    error: (status, message) => {
                        reject({ status: status.status, message: status.statusText });
                    }
                });
            });
        },
        getTableInfo(){
            let incident_url = "http://localhost:8001/incidents?limit=1000";
            let neighborhood_url = "http://localhost:8001/neighborhoods";
            let code_url = "http://localhost:8001/codes"
            Promise.all([this.getJSON(incident_url),this.getJSON(neighborhood_url),this.getJSON(code_url)])
            .then((results) => {
                this.incidents = JSON.parse(JSON.stringify(results[0]));            
                this.neighborhoods = JSON.parse(JSON.stringify(results[1]));
                this.codes_json = JSON.parse(JSON.stringify(results[2]));
            })
            .catch((error) =>{
                alert("Something went wrong");
                console.log("Error:", error);
            })
        },
        getType(code) {
            for (const value in this.codes_json) {
                    
                if (this.codes_json[value].code == code) {
                    return this.codes_json[value].incident_type;
                }
            }
        }, 
        getNeighborhood(neighborhood_number) {
            for (const value in this.neighborhoods) {  
                if (this.neighborhoods[value].neighborhood_number == neighborhood_number) {
                    return this.neighborhoods[value].neighborhood_name;
                }
            }
        },
        replaceX(block) {
            let split_block = block.split(" ");
            split_block[0] = split_block[0].replaceAll("X", 0);
            let new_block = "";
            for(let i=0; i<split_block.length; i++){
                new_block += split_block[i] +' ';
            }
            return new_block;
        },
        delete_incident(case_number){
            console.log(case_number);
            $.ajax({
                url: "http://localhost:8001/remove-incident",
                contentType: 'application/json',
                type: 'DELETE',
                data: "{\"case_number\":"+String(case_number)+"}",
                success: function(response) {
                  // handle success
                  location.reload();
                },
                error: function(error) {
                  // handle error
                  console.log("whoops");
                }
            });
        },
        updateTextBox() {
            let coords = this.leaflet.map.getBounds();
            let centerCoords = coords.getCenter();
            let url = 'https://nominatim.openstreetmap.org/reverse?format=json&lat=<1value>&lon=<2value>';
            // on mouse up thing - map.on('mouseup,' onMouseUp)
            
            // map.on('mouseup', function(e) {

            // });
            
            let newUrl = url.replace('<1value>', centerCoords.lat);
            newUrl = newUrl.replace('<2value>', centerCoords.lng);
            console.log(newUrl);
            let req = {
                    url: newUrl,
                    dataType: 'json',
                    success: this.latLongData
                }
            $.ajax(req);
            
        

        },
        latLongData(data) {
            console.log(data);
            this.textbox = data.display_name;
            document.getElementById("input-box").value = this.textbox;
            
            
        },
        getMapBoundaries() {
            let bound = this.leaflet.map.getBounds();
            let northWest = bound.getNorthWest();
            let southEast = bound.getSouthEast();
            // Loop through neighborhood marker to check if coordinate is out of bound.
            // If out of bound, then set onMap boolean to false
            for (let i = 0; i < this.leaflet.neighborhood_markers.length; i++) {
                    if (this.leaflet.neighborhood_markers[i].location[0] > northWest.lat) {
                        this.leaflet.neighborhood_markers[i].onMap = false;
                    }
                    if (this.leaflet.neighborhood_markers[i].location[1] < northWest.lng) {
                        this.leaflet.neighborhood_markers[i].onMap = false;
                    }
                    if (this.leaflet.neighborhood_markers[i].location[0] < southEast.lat) {
                        this.leaflet.neighborhood_markers[i].onMap = false;
                    }
                    if (this.leaflet.neighborhood_markers[i].location[1] > southEast.lng) {
                        this.leaflet.neighborhood_markers[i].onMap = false;
                    }
            }
        }

    },
    mounted() {
        this.leaflet.map = L.map("leafletmap").setView([this.leaflet.center.lat, this.leaflet.center.lng], this.leaflet.zoom);
        L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
            attribution: "&copy; <a href=\"https://www.openstreetmap.org/copyright\">OpenStreetMap</a> contributors",
            minZoom: 11,
            maxZoom: 18
        }).addTo(this.leaflet.map);
        this.leaflet.map.setMaxBounds([[44.883658, -93.217977], [45.008206, -92.993787]]);
        
        let district_boundary = new L.geoJson();
        district_boundary.addTo(this.leaflet.map);
        this.getJSON("/data/StPaulDistrictCouncil.geojson").then((result) => {
            // St. Paul GeoJSON
            $(result.features).each((key, value) => {
                district_boundary.addData(value);
            });
        }).catch((error) => {
            console.log("Error:", error);
        });
        this.getTableInfo();
        this.drawMarker();
        this.leaflet.map.on('mouseup', this.updateTextBox);
        this.leaflet.map.on('zoom', this.updateTextBox);
    },
    
    components: { 
        new_incident,
        about
     }
     
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
                <div style = "float:left; left:80px; top:20px; padding-right: 50px;">
                    <!--Input TextBox-->
                    <input class="e-input" id="input-box" type="text" v-model="location" placeholder="Enter Location or Coord.">
                    <button type="button" class="button" @click="searchLocation">Go</button><br>
                    
                </div>
                <div id="leafletmap" class="cell auto"></div>
                
            </div>
        </div> 
        <br/><br/>
        <div class="center border ">
            <table style="left:1em;">
                <thead>
                    <tr>
                    <th width="100px">Case Number</th>
                    <th width="100px">Incident Type</th>
                    <th width="100px">Incident</th>
                    <th width="100px">Date</th>
                    <th width="100px">Time</th>
                    <th width="100px">Police Grid</th>
                    <th width="100px">Neighborhood Name</th>
                    <th width="150px">Block</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(value, key) in this.incidents" :key="key">
                            <td>{{ value.case_number }}</td>
                            <td v-text="getType(value.code)"></td> 
                            <td>{{ value.incident }}</td>
                            <td>{{ value.date }}</td>
                            <td>{{ value.time }}</td>
                            <td>{{ value.police_grid }}</td>
                            <td v-text="getNeighborhood(value.neighborhood_number)"></td>
                            <td v-text="replaceX(value.block)"></td>
                            <td><input type="submit" value="Delete" class="button alert" @click="delete_incident(value.case_number)"></td>
                    </tr> 
                </tbody>
            </table>
        </div>
    </div>
    <div v-if="view === 'new_incident'">
        <new_incident />
    </div>
    <div v-if="view === 'about'">
        <about />
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
.center {
  margin: auto;
  width: 65%;
}
.border {
  border: 3px solid black;
}
</style>

