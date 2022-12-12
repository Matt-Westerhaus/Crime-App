<script>
import $ from 'jquery'
export default {
    data() {
    },
    methods: {

    }
    
}
</script>

<template>
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
                        <td><input type="submit" value="Delete" class="button alert"></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<style>

</style>