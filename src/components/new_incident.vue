<script>
import $ from 'jquery'
export default {
    data() {
        return {
            case_number: "",
            date: "",
            time: "",
            code: 0,
            incident: "",
            police_grid: 0,
            neighborhood_number: 0,
            block: ""
        }
    },
    methods: {
        test() {
            var queryString = $('#submit').serialize();
            console.log(queryString);
        }
    }
    
}
</script>

<template>
    <!-- Replace this with your actual form: can be done here or by making a new component -->
    <div class="grid-container">
        <div class="grid-x grid-padding-x">
            <h1 class="cell auto">New Incident Form</h1>
            <form id="form_submission">
                <label for="case_number">Case Number:</label><br>
                <input type="text" id="case_number" required><br>
                <label for="date_time">Date & Time:</label><br>
                <input type="datetime-local" id="date_time" required><br>
                <label for="code">Code:</label><br>
                <input type="number" id="code" required><br>
                <label for="incident">Incident:</label><br>
                <input type="text" id="code" required><br>
                <label for="police_grid">Police Grid:</label><br>
                <input type="number" id="police_grid" required><br>
                <label for="neighborhood_number">Neighborhood Number:</label><br>
                <input type="number" id="neighborhood_number" required><br>
                <label for="block">Block:</label><br>
                <input type="text" id="block" required><br>

                <input type="submit" class="button success" id="submit" value="Submit" @click="test('submit')">

            </form>
        </div>
    </div>
</template>

<style>

</style>