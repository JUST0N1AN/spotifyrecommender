<template>
<nav>
    <div class="nav-wrapper green accent-4">
      <a href="#" class="brand-logo center" style="font-size:medium">Spotify Recommender</a>
    </div>
</nav>
  <router-view/>
</template>

<script>
import M from 'materialize-css'

export default{
  mounted(){
    M.AutoInit();
  }
}
</script>


<style>
body{
  font-family:'Garet', sans-serif;
  background:#37474f;
}
</style>

