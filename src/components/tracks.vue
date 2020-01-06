<template>
  <div class="tracks-wrapper">
      <div class="container">
        <div class="content">
            <div class="item-1" style="position:fixed;">
                <Playlist v-bind:playing ="playing" v-bind:songs="tracks" :play ="play" :pause ="pause" ></Playlist>
            </div>

            <div class="item-2 actual">
                <Songs v-bind:songs="tracks" :setPlaying = "setPlaying" :play ="play" :pause ="pause" :addToPlaylist = "addToPlaylist" v-bind:audio="audio"></Songs>
            </div>
        </div>
        
      </div> 
  </div>
  
</template>

<script>
    import Playlist from './playlist.vue';
    import Songs from './songs.vue';
    export default {
        name:'Tracks',
        props:[
            "tracks",
            "playing",
            "setPlaying",
            "play",
            "pause",
            "addToPlaylist",
            "playlistPlay",
            "audio"
        ],
        data (){
           return {
               trackList:this.tracks
           }
        },
        components: {
            Playlist,
            Songs
        },
        created(){
            // console.log(this.tracks)
        }
    }
    
</script>

<style>
    /* .tracks-wrapper .content{
        display: flex;
        justify-content: space-between;
    } */
    .tracks-wrapper .item-1{
        width:20%;
        /* position: fixed; */
    }
    .tracks-wrapper .item-2.actual{
        width:100%;
        padding-left:300px;
    }
</style>