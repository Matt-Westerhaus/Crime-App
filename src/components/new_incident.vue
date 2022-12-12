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

                <input type="submit" class="button success">
                
            </form>
        </div>
    </div>
</template>

<style>

</style>