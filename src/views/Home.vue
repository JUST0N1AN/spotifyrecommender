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
      <a class="waves-effect waves-light btn modal-trigger green accent-4" style="margin-left:5px;"  @click="getRec()">Get Recommendations</a>
      </div>
</form>
<div class="row"  >
  <div class="col s6 push-s3">
    <ul class="collection" style="overflow-y: auto;" >
      
      <li v-for="(i, index) in songs" :key="index" class="collection-item">
        <div  class="card green accent-4">
        <div class="card-content white-text">
          <span class="card-title">{{ i.name }}</span>
          <p>Year: {{i.year}}</p>
          <p>Artists: {{i.artists}}</p>
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


export default {
    data(){
        return{
            song:null,
            year:null,
            songs: [],
        }
    },
    methods:{
        async getRec(){
            this.song = document.getElementById("song").value;
            this.year = document.getElementById("year").value;
            this.year = parseInt(this.year);
            console.log(this.year);
            console.log(this.song); //Please change url to the local IP with /reccomend at the end for local testing
            var axios = require('axios');
var data = JSON.stringify({
  "name": this.song,
  "year": this.year
});

var config = {
  method: 'post',
  url: 'http://127.0.0.1:5000/reccomend',
  headers: { 
    'Content-Type': 'application/json'
  },
  data : data
};

const temp = await axios(config)
.then(async (response) => {
  console.log(JSON.stringify(response.data));
  this.songs = response.data;
  for(let i=0; i<this.songs.length;i++){
      this.songs[i].artists = this.songs[i].artists.replaceAll('[','');
      this.songs[i].artists = this.songs[i].artists.replaceAll(']','');
      this.songs[i].artists = this.songs[i].artists.replaceAll(']','');
      this.songs[i].artists = this.songs[i].artists.replaceAll("'",'');
  }
})
.catch(function (error) {
  console.log(error);
});
console.log(temp);

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
