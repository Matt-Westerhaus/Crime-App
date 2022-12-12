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
                <th>Tool</th>
                <th>How It Was Used</th>
              </tr>
              <tr>
                <td>Vue.js  </td>
                <td>Explain here</td>
              </tr>
              <tr>
                <td>Foundation</td>
                <td>Explain here</td>
              </tr>
              <tr>
                <td>Tool</td>
                <td>Explain here</td>
              </tr>
              <tr>
                <td>Tool</td>
                <td>Explain here</td>
              </tr>
              <tr>
                <td>Tool</td>
                <td>Explain here</td>
              </tr>

            </table>

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