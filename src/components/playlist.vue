<template>
    <div class="playlist-wrapper">
        <div class="playlist-heading">
            <h6>Playlist 
                <!-- (5)  -->
                </h6> 
                    <span class="icon">
                        <PlayPauseBtn :play ="playlistPlayAll" :pause ="pause" v-bind:index ="0" v-bind:song="songs"></PlayPauseBtn> 
                        <span class="playlist-playall">play all</span>
                    </span>
        </div> 

        <ul v-for="(song, index) in songs" v-if="song.playlist">
            <li>{{song.title}} 
                <span>
                    
                    <div class="playpause-btn-container">
                        <span v-if="!song.playing"><i class="fa fa-play playbtn" @click="play(index,another)"></i></span>
                        <span v-if="song.playing"><i class="fa fa-pause pausebtn" @click="pause(index)"></i></span>
                    </div>
                    <!-- <span v-if="!song.playing"><i class="fa fa-play" @click="playlistPlay(index)"></i></span>
                    <span v-if="song.playing"><i class="fa fa-pause" @click="pause(index)"></i></span> -->
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
import PlayPauseBtn from './playpause';
export default {
    name:'Playlist',
    props:['playing', "songs", "play", "pause"],

    data (){
        return{
            
        }
    },
    methods:{
        another (){
            console.log("New")
        },
         playlistPlayAll(){
            let arr = []
             this.songs.forEach((item , i)=>{
                 if(item.playlist){
                     arr.push(i)
                    //  if(){

                    //  }
                     this.play(arr[0], this.another)
                    
                 }
             })
         }

        
    },
    components:{
        PlayPauseBtn
    },
}
</script>

<style>
    .playlist-wrapper{
        background:white;
        padding:20px 11px;
        border-radius: 4px;
        max-height:400px;
        overflow-y:scroll;
    }
    .playlist-wrapper .playlist-heading{
        display: flex;
        justify-content: space-betweenl
    }
    .playlist-wrapper h6{
       margin-bottom: 25px;
       width:75%;
    }
    .playlist-wrapper .playlist-heading .icon{
        margin-right:10px;
        width:25%;
    }
    .playlist-wrapper span i{
        /* width:fit-content;
        margin:0 auto; */
        float: right;
        display: block;
        cursor:pointer;
    }

    .playlist-wrapper ul{
        margin:0;
        padding:0;
    }
    .playlist-wrapper ul li{
        padding:10px 0;
    }
    .playlist-wrapper ul li span{
       float: right;
        margin-right:10px;
    }
    .playlist-playall{
        display: block;
        font-size:10px;
    }
</style>