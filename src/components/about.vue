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
            <h1 class="cell text-center">About the Project</h1>
        </div>
        <br/>
    </div>
    <hr/>
    
    <div class="grid-container">
       
        <div class="grid-x grid-padding-x">
            <h2 class="cell text-center">Tools Used</h2>
        </div>
        <div class="text-center">
            <table>
              <tr>
                <th style="width:25%">Tool</th>
                <th>How It Was Used</th>
              </tr>
              <tr>
                <td>Vue JS  </td>
                <td>Vue JS is a JavaScript framework that makes it much easier to make your website responsive. We used Vue within each of our buttons 
                    to accomlish things like changing the page in the menu or accessing the database in submit/delete buttons. </td>
              </tr>
              <tr>
                <td>Foundation</td>
                <td>Foundation is a web design framework that we used to format our pages more uniformily and more easily. It contains many premade css classes
                    that we were able to take advantage of for the making of the front-end aspect of the website.
                </td>
              </tr>
              <tr>
                <td>Nominatim API</td>
                <td>The Nominatim API allows you to search for locations by name, or retrieve a location's name based on lat/long coordinates. We used this 
                    in our search box to allow the user to input where to look on the map.
                </td>
              </tr>
              <tr>
                <td>Leaflet</td>
                <td>This API allows you to render interactive maps in your web page as well as overlay data on top of the map. 
                    The map can be modified either by user interaction or by JavaScript commands. We used this to display the map on the main page</td>
              </tr>
              <tr>
                <td>St. Paul Crime</td>
                <td>This is an api that we made earlier in the semester using public data on crime in St. Paul Minnesota. We used it to populate our map and table of 
                    incident results with their filters. We also used it when deleting an incident or submitting a new one.</td>
              </tr>

            </table>
            <!-- What else???-->
        </div>
           
    </div>

    <div class="grid-container video">
        <div class="grid-x grid-padding-x">
            <h2 class="cell text-center">Video Demo</h2>
        </div>
        
        <div class="grid-x grid-padding-x">
            <!-- Just a placeholder video-->
            <iframe  height="500" width="100%" src="https://www.youtube.com/embed/tgbNymZ7vqY" allowfullscreen="true">
            </iframe>
        </div>
    </div>


    <div class="grid-container">
        <br/>
        <br/>
        <div class="grid-x grid-padding-x">
            <h2 class="cell text-center">Interesting Findings</h2>
        </div>
    </div>

    <div class="grid-container">

<h2 class="cell text-center"> Authors</h2>  
<div class="grid-x grid-padding-x">

    <div class="cell center small-6 large-6 ">
        <h3>Nolan Foy</h3>
        <p></p>
        
    </div>
    <div class="cell small-6 large-6 center"><img src ="image here" class="floatleft" alt="Picture of Nolan"/></div> 
</div>
<br/>


<div class="grid-x grid-padding-x">
    
    <div class="cell small-12 large-6 center ">
    <h3>Owen Xiong</h3>
    </div>
    <div class="cell small-12 large-6 center"><img src ="image here" class="floatleft" alt="Picture of Owen"/></div> 
</div>
<br/>

<div class="grid-x grid-padding-x">
    
    <div class="cell center small-6 large-6 ">
        <h3>Matt Westerhaus</h3>
        <p>Hello, I am a senior majoring in Computer Science and minoring in Catholic Studies here at St Thomas. I enjoy being outside playing sports, camping, 
            or just exploring. I also enjoy playing video games, listening to music or just hanging out with people. I am from Chanhassen, MN which is about 30 
            minutes southwest of St. Thomas. 
        </p>
        <p>
            After graduating in December I will start working at Optum in July 2023 in their Technology Development Program (TDP). I interned with them this 
            past summer and enjoyed it so I am super thrilled to be going back full time. 
        </p>
        Here is my <a href="https://github.com/Matt-Westerhaus/Matt-Westerhaus"> Github</a>
    </div>
    <div class="cell small-6 large-6 center"><img src ="images\matt_image.jpg" id="float-center" alt="Picture of Matt"/></div> 
</div>
</div>
    
</template>

<style>
h1,
h2,
h3,
p {
    font-family: Bookman, URW Bookman L, serif;
}
img {
    height: 300px
}
</style>