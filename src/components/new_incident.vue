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
        submitForm() {
            $.ajax({
                url: 'http://localhost:8001/new-incidents',
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
            // let req = {
            //         url: 'https://localhost8001/new-incident/' + this.case_number + this.date_time + this.code + this.incident + this.police_grid + this.neighborhood_number + this.block,
            //         dataType: 'json',
                    
            //         success: function(response) {
            //             alert("added successfully");
            //         },
            //         error: function (xhr, thrownError) {
            //             alert(xhr.status);
            //             alert(thrownError);
            //             alert("NOPE");
            //         }
            //     }
            //     $.ajax(req);
            // let url= 'https://localhost8001/new-incident/' + this.case_number + this.date_time + this.code + this.incident + this.police_grid + this.neighborhood_number + this.block;
            // getJSON(url);

        }
    }
    
}

</script>

<template>

    <!-- Replace this with your actual form: can be done here or by making a new component -->
    <div class="grid-container">
        <h1 class="cell auto">New Incident Form</h1>
        <div class="grid-x grid-padding-x">
            
            <br>
            <form class="medium-3 cell" id="formSubmit" >
                <label for="case_number">Case Number:</label>
                <input type="text" id="case_number" v-model="case_number" required>
                <label for="date_time">Date & Time:</label>
                <input type="datetime-local" id="date_time" v-model="date_time" required>
                <label for="code">Code:</label>
                <input type="number" id="code" v-model="code" required>
                <label for="incident">Incident:</label>
                <input type="text" id="incident" v-model="incident" required>
                <label for="police_grid">Police Grid:</label>
                <input type="number" id="police_grid" v-model="police_grid" required>
                <label for="neighborhood_number">Neighborhood Number:</label>
                <input type="number" id="neighborhood_number" v-model="neighborhood_number" required>
                <label for="block">Block:</label>
                <input type="text" id="block" v-model="block" required>
                


                <input type="button" class="button success" value="Submit" @click="submitForm()">

            </form>
        </div>
    </div>
</template>

<style>

</style>