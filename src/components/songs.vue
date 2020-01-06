<template>
    <div>
        <div class="songs-wrapper" v-for="(song, index) in songs">
            <div class="tracks">
                <div class="item-1">
                    <img :src = song.img alt="">
                    <div class="meta">
                        <h6>{{song.artist}}</h6>
                        <p>{{song.title}}</p>
                    </div>
                </div>

                <div class="item-2">
                    <p>{{song.plays}}</p>
                </div>

                <div class="item-3">
                    <button @click="addToPlaylist(index)">Add to playlist</button>
                </div>

                <div class="item-4">
                    <PlayPauseBtn :play ="play" :pause ="pause" v-bind:index ="index" v-bind:song="song" v-bind:audio="audio"></PlayPauseBtn>

                    <!-- <span v-if="!song.playing"><i class="fa fa-play" @click="play(index)"></i></span>
                    <span v-if="song.playing"><i class="fa fa-pause" @click="pause(index)"></i></span> -->
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import PlayPauseBtn from './playpause';
export default {
    name:'Songs',
    props:['songs', 'setPlaying', "play", "pause", "addToPlaylist",],

    data (){
        return{
            // songs:["1","2","3","4","5"],
            songList:this.songs,
            playing:'',
            audio : new Audio()
        }
    },
    
    methods:{
        
        // pause(item){
        //     this.audio.pause()
        //     item.playing = false;
        //     console.log(this.audio.paused)
        // }
    },
    components:{
        PlayPauseBtn
    },
    created(){
            // console.log(this.songs)
        }
}
</script>

<style>
    .songs-wrapper{
        background:white;
        padding:10px 15px;
        border-radius: 4px;
        margin-bottom:15px;
       
    }
    .songs-wrapper .tracks{
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .songs-wrapper .item-1{
        display: flex;
        width:40%;
    }
    .songs-wrapper .item-1 img{
        width:60px;
        height:60px;
        margin-right: 10px;
        align-items: center;
    }
    .songs-wrapper .item-1 h6{
        margin-bottom:5px;
    }
    .songs-wrapper .item-1 p{
        margin-bottom:0px;
    }
    .songs-wrapper .item-2{
        width:20%;
    }
    .songs-wrapper .item-3{
        width:20%;
    }
    .songs-wrapper .item-3 button{
        background:#dffbff;
        border:none;
        padding:5px 15px;
        border-radius: 15px;
        color:#527e85;
        outline:none;
    }
    .songs-wrapper .item-4{
        width:10%;
    }
    /* .songs-wrapper .item-4 span{
        float: right;
        margin-right:5px;
    } */
</style>