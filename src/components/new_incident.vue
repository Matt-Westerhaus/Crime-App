<script>
import $ from 'jquery'
export default {
    data() {
        return {
            case_number: "",
            date_time: "",
            code: 0,
            incident: "",
            police_grid: 0,
            neighborhood_number: 0,
            block: ""
        }
    },
    methods: {
        submitForm() {
            $.ajax({
                url: 'http://localhost:8001',
                type: 'PUT',
                data: {
                    case_number: this.case_number,
                    date: this.date_time.toString().split("T")[0], 
                    time: this.date_time.toString().split("T")[1],
                    code: this.code,
                    incident: this.incident,
                    police_grid: this.police_grid,
                    neighborhood_number: this.neighborhood_number,
                    block: this.block
                },
                success: function(response) {
                  alert("Added succesfully!");
                },
                error: function (xhr, thrownError) {
                    alert(xhr.status);
                    alert(thrownError);
                }
            });

        }
    }
    
}

</script>

<template>

    <!-- Replace this with your actual form: can be done here or by making a new component -->
    <div class="grid-container">
        <div class="grid-x grid-padding-x">
            <h1 class="cell auto">New Incident Form</h1>
            <form id="formSubmit">
                <label for="case_number">Case Number:</label><br>
                <input type="text" id="case_number" v-model="case_number" required><br>
                <label for="date_time">Date & Time:</label><br>
                <input type="datetime-local" id="date_time" v-model="date_time" required><br>
                <label for="code">Code:</label><br>
                <input type="number" id="code" v-model="code" required><br>
                <label for="incident">Incident:</label><br>
                <input type="text" id="code" v-model="incident" required><br>
                <label for="police_grid">Police Grid:</label><br>
                <input type="number" id="police_grid" v-model="police_grid" required><br>
                <label for="neighborhood_number">Neighborhood Number:</label><br>
                <input type="number" id="neighborhood_number" v-model="neighborhood_number" required><br>
                <label for="block">Block:</label><br>
                <input type="text" id="block" v-model="block" required><br>
                


                <input type="button" class="button success" value="Submit" @click="submitForm()">

            </form>
        </div>
    </div>
</template>

<style>

</style>