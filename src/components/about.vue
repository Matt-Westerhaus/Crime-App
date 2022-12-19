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
            <!-- Just a placeholder video
            <iframe  height="500" width="100%" src="https://youtu.be/vRfiC2n1SjE" allowfullscreen="true">
            </iframe> -->
            <iframe width="100%" height="500" src="https://www.youtube.com/embed/vRfiC2n1SjE" title="YouTube video player" frameborder="0" 
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
            </iframe>
        </div>
    </div>


    <div class="grid-container">
        <br/>
        <br/>
        <div class="grid-x grid-padding-x">
            <h2 class="cell text-center">Interesting Findings</h2>
            <p>1. The first thing that I found interesting (which I wouldn't have expected to find interesting) was the way that the adresses of the crimes were
                input. Just blocks and neighborhoods along with the police grid that it took place in. I wouldn't expect that the neighborhood would be an important
                piece of information. <br>
                2. Another that was interesting, but more upsetting, was when I looked at the crimes in my neighborhood. Unfotunately, a lot of the crimes were theft. 
                Lots of auto theft, burglary, and shoplifting going on in Union Park.<br>
                3. I was also surprised to see not as many crimes in Midway as I expected just because of what you hear about it. In general, the more west you go,
                 the less crime there is.<br>
                4. It was also surprising to see the second fewest amount of crimes occurred in the largest neighborhood in terms of area. It is larger because of Pig Eyes Regional Park 
                and the large lake that resides in it, but it was surprising nonetheless.<br>
                5. It was nice to see that Como Park had the least amount of crimes. I was hoping there wouldn't be crimes at the zoo, that would be sad for all the animals there.<br>
                6. The last thing that I found that was surprising was about the functionality of the program and how nomination works. For the most part, when the center of the 
                map changed and the search bar changed with it, there would just be obscure adresses and streets. However, there were spots where it would identify landmarks or 
                other specific buildings and sites. This was cool to see that they were recognizing these things sometimes.
            </p>
        </div>
    </div>

    <div class="grid-container">

<h2 class="cell text-center"> Authors</h2>  
<div class="grid-x grid-padding-x">

    <div class="cell center small-6 large-6 ">
        <h3>Nolan Foy</h3>
        <p>Hi, I am Nolan and I am a senior majoring in Computer Science at the University of St. Thomas. I love playing sports, playing video games, going out with my
            friends, and watching the Vikings. I am from Andover, MN just 30 minutes north of here. 
        </p>
        <p>I will be graduating in December and will start working with Optum in late January in their Technology Development Program after I interned with them over the summer. 
            Hopefully I will be seeing my fellow teammate Matt there, as we are both going down the same route.
        </p>
        
    </div>
    <div class="cell small-6 large-6 center"><img src ="images/nolan_image.JPG" class="floatleft" alt="Picture of Nolan"/></div> 
</div>
<br/>


<div class="grid-x grid-padding-x">
    
    <div class="cell small-12 large-6 center ">
    <h3>Owen Xiong</h3>
    <p>Hello, I'm Owen Xiong and I am a senior this year majoring in Commputer Science. I am first generation college student and also the oldest child of all my siblings.
        I enjoy playing video games, working out, hanging out with friends, and volleyball. An interesting factt about me is that I was born in Thailand and my family migrated
        to the United States when I was about 3-4 years old. 
    </p>
    <p>
        After graduation, I will be starting work at Best Buy Headquarter in January 2023 with the Database team at Best Buy.
         I believe I will be working most of weekdays remote, but I am excited to be working with my team again.
    </p>
    </div>
    <div class="cell small-12 large-6 center"><img src ="images/owen.jpeg" class="floatleft" alt="Picture of Owen"/></div> 
</div>
<br/>

<div class="grid-x grid-padding-x">
    
    <div class="cell center small-6 large-6 ">
        <h3>Matt Westerhaus</h3>
        <p>Hello, I am a senior majoring in Computer Science and minoring in Catholic Studies here at St Thomas. I enjoy being outside playing sports, cards, camping, 
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