<template>
  <div class="container">
    <div class="row valign center">
    <div class="col s12 ">
      <div class="card-panel blue-grey darken-4 ">
        <span>
            <form>
                <h3 class="form__title">Choose Your Song</h3>
      <div class="row">
        <div class="input-field col s10 push-s1">
          <input  id="song" type="text" class="validate">
          <label for="song">Please Enter Correct Song Name</label>
        </div>
        </div>
        <div class="row">
        <div class="input-field col s10 push-s1">
          <input id="year" type="number" class="validate">
          <label for="year">Song Year</label>
        </div>
      </div>
      
      <div class="valign center">
      <button class="waves-effect waves-light btn modal-trigger green accent-4" style="margin-left:5px;"  @click="getRec()">Get Recommendations</button>
      </div>
</form>
<div class="row"  >
  <div class="col s6 push-s3">
    <ul class="collection" style="overflow-y: auto;">
      
      <li v-for="(i, index) in songs" :key="index" class="collection-item">
        <div  class="card green accent-4">
        <div class="card-content white-text">
          <span class="card-title">{{ i.name }}</span>
          <p>Year: {{i.year}}</p>
          <p>Artists: <ul>
            <li v-for="(i, index) in i.artists" :key="index" >{{i}}</li>
            </ul></p>
            <br>
        </div>
      </div>
      </li>
    </ul>
</div>
</div>
        </span>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios';

export default {
    data(){
        return{
            song:null,
            year:null,
            songs:[],
        }
    },
    methods:{
        getRec(){
            this.song = document.getElementById("song").value;
            this.year = document.getElementById("year").value;
            this.year = parseInt(this.year);
            axios.get(`https://recommend-intus.herokuapp.com/reccomend`,{
                params: {
                    "name": this.name,
                    "year": this.year
                }
            });
        }
    },
}
</script>

<style>
body{
    color:white;
}
.input-field label {
     color:white;
   }
</style>

// {
// "name": "Come As You Are",
// "year":1991
// }