<template>
  <div class="playpause-btn-container">
      <span v-if="!song.playing"><i class="fa fa-play playbtn" @click="play(index)"></i></span>
      <span v-if="song.playing"><i class="fa fa-pause pausebtn" @click="pause(index)"></i></span>
  </div>
</template>

<script>
export default {
    name:"PlayPauseBtn",
    props:["play", "pause", "index","song",
    "audio"]
}
</script>

<style>
.playpause-btn-container{
  display: inline;
}
.playbtn, .pausebtn{
    color:#527e85;
    cursor:pointer;
    transition: all ease .1s;
    font-size:18px;
}
.playbtn:hover,.pausebtn:hover{
    color:#dffbff;
}
</style>