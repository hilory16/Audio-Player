<template>
  <div class="playing-wrapper">
      <div class="container">
          <div class="content">
                <div class="item-1">
                    <img :src = current[0].img alt="">
                    <div class="meta">
                        <h6>{{this.current[0].artist}}</h6>
                        <p>{{current[0].title}}</p>
                    </div>
                </div>
                  
                <div class="item-2">
                    <span><i class="fa fa-step-backward my-prev"  @click="prevSong(current[1])"></i></span>
                    <PlayPauseBtn :play ="play" :pause ="pause" v-bind:index ="current[1]" v-bind:song="current[0]"></PlayPauseBtn>
                    <span><i class="fa fa-step-forward my-next" @click="nextSong(current[1])"></i></span>
                    <span class="seek-bar">
                        <input type="range" id="seek" value="0" max="" v-model="seek" v-on:change="changeSeek"/>
                        <span><span>{{currentTime}} </span>/ {{totalTime}}</span>
                    </span>
                    <!-- <span class="seek"> <span class="lenght"></span></span> -->
                </div>

                <div class="item-3">
                    
                    <span><i class="fa fa-volume-up"></i></span> 0<input type="range" class="volume" name="volume" min="0" max="100" v-model="volume" v-on:change="setVolume"/> 100
                    <!-- {{currentPlay}} -->
                </div>
          </div>    
      </div>
  </div>
</template>

<script>
import PlayPauseBtn from './playpause';
export default {
    name:'Playing',
    props:['current',"play", "pause", "tracks", "nextSong", "prevSong", "audio"],
    data (){
        return {
            currentPlay:this.current,
            volume:100,
            currentTime: "00:00",
            totalTime: "",
            seek: this.audio.currentTime
        }
    },
    methods:{
        me (){
            
                console.log(this.current[0].playing)
            
        },
        setVolume (){
            let newVolume = this.volume/100;
            this.audio.volume = newVolume;
            // console.log(this.current)
        },
        changeSeek (){
            const key =  this.audio.duration / 100
            const pos = Math.floor(this.seek) * key
           
            this.audio.currentTime = pos
            this.getcurrentTime()
            console.log(pos)
        },
        getcurrentTime (){
            let time = this.audio.currentTime
            let min = Math.floor(time / 60)
            let sec =  Math.floor(time % 60)

            min = min < "10" ? `0${min}`: min
            sec = sec < "10" ? `0${sec}`: sec
            
             this.currentTime =  `${min}:${sec}`
           
        },
         getTotalTime (){
            let time = this.audio.duration
            let min = Math.floor(time / 60)
            let sec =  Math.floor(time % 60)

            min = min < "10" ? `0${min}`: min
            sec = sec < "10" ? `0${sec}`: sec
            
             this.totalTime =  `${min}:${sec}`
        }
    },
    components:{
        PlayPauseBtn
    },
    created (){
        setInterval(()=>{
            
           this.getcurrentTime ()

           this.getTotalTime ()
           this.seek = this.audio.currentTime/ this.audio.duration * 100
        }, 1000)
    }
}
</script>
    
<style>
    .playing-wrapper{
        background:white;
        width:100%;
    }
    .playing-wrapper .content{
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding-top:25px;
        padding-bottom:25px
    }
    .playing-wrapper .item-1{
       display: flex;
       align-items: center;
       width:24%;
    }
    .playing-wrapper .item-1 img{
        width:80px;
        height:80px;
        margin-right:20px;
    }
    .playing-wrapper .item-2{
        width:50%;
    }
    .playing-wrapper .item-2 .seek{
        height:14px;
        padding:2px;
        margin-left:10px;
        width:80%;
        background:#527e85;
        display: inline-block;
        border-radius: 4px;
    }
    .playing-wrapper .item-2 .seek .lenght{
        height:10px;
        width:55%;
        display: block;
        background:white;
    }
    .my-prev{
         margin-right:8px;
    }
    .my-next{
         margin-left:8px;
    }
    .my-prev, .my-next{
        color:#527e85;
        cursor:pointer;
        transition: all ease .1s;
        font-size:18px;
       
    }
    .my-prev:hover,.my-next:hover{
        color:#dffbff;
    }
    .item-2 .seek-bar{
        vertical-align: text-bottom;
    }
    #seek{
        -webkit-appearance: none;
        border:1px solid #000;
        height:5px;
         width:85%;
        vertical-align: center;
        border-radius: 20px;
        outline:none;
        background:#527e85;
        margin-left:10px;
        cursor: pointer;
    }
    #seek::-webkit-slider-thumb {
        -webkit-appearance: none;
        width:15px;
        height:15px;
        border:1px solid #000;
        background:white;
        border-radius: 50%;
    }
    .volume{
        -webkit-appearance: none;
        border:1px solid #000;
        height:5px;
        width:150px;
        vertical-align: center;
        border-radius: 20px;
        outline:none;
        background:#527e85;
        margin-left:10px;
        cursor:pointer;
    }
    .volume::-webkit-slider-thumb {
        -webkit-appearance: none;
        width:15px;
        height:15px;
        border:1px solid #000;
        background:white;
        border-radius: 50%;
    }
    /* .item-3{

    } */
</style>