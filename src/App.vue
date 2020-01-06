<template>
  <div id="app">
    <div class="top">
      <Playing v-bind:current ="current" v-bind:tracks="tracks" :play ="play" :pause ="pause" :nextSong = "nextSong" :prevSong = "prevSong" v-bind:audio="audio"></Playing>
    </div>

    <div class="bottom">
      <Tracks
       :setPlaying = "setPlaying"
       :play ="play"
       :pause ="pause"
       :addToPlaylist = "addToPlaylist"
       v-bind:tracks="tracks"
       v-bind:audio="audio"
       ></Tracks>
    </div>
  </div>
</template>

<script>
import Placard from './components/Placard.vue';
import Playing from './components/playing.vue';
import Tracks from './components/tracks.vue';
let song = '';
export default {
  name: 'app',
  data () {
    return {
      currentTrack:0,
      tracks:[
        {
            title:'Billionaire',
            artist:'Teni',
            src:'src/tracks/teni.mp3',
            img:'src/img/teni.jpg',
            plays:"1,678,965",
            genre:'hip-hop',
            playlist:false,
            playing:false,
            paused:null

        },
        {
            title:'I Never Know Say',
            artist:'Timi Dakolo',
            src:'src/tracks/timi.mp3',
            img:'src/img/timi.jpg',
            plays:"123,456",
            genre:'RnB',
            playlist:false,
            playing:false,
            paused:null
        },
        {
            title:'Dangote',
            artist:'Burna Boy',
            src:'src/tracks/burnadangote.mp3',
            img:'src/img/burna-dangote.jpg',
            plays:"559,500",
            genre:'pop',
            playlist:false,
            playing:false,
            paused:null
        },
        {
            title:'Ye',
            // Fireboy-Jealous.mp3
            artist:'Burna Boy',
            src:'src/tracks/burna_ye.mp3',
            img:'src/img/burna_ye.jpg',
            plays:"890,879",
            genre:'Reggae',
            playlist:false,
            playing:false,
            paused:null
        },
        {
            title:'Jealous', 
            artist:'FireBoy DML',
            src:'src/tracks/Fireboy-Jealous.mp3',
            img:'src/img/fireboy-jealous.jpg',
            plays:"46,900",
            genre:'Reggae',
            playlist:false,
            playing:false,
            paused:null
        },
        {
            title:'Uyo Meyo', 
            artist:'Teni',
            src:'src/tracks/Teni-Uyo-Meyo.mp3',
            img:'src/img/Teni-Uyo-Meyo.jpg',
            plays:"29,890",
            genre:'Fuji',
            playlist:false,
            playing:false,
            paused:null
        },
        {
            title:'Loving', 
            artist:'Falz',
            src:'src/tracks/Falz-Loving.mp3',
            img:'src/img/Falz-Loving.jpg',
            plays:"345,666",
            genre:'Hip Hop',
            playlist:false,
            playing:false,
            paused:null
        },
        {
            title:"That's how star do", 
            artist:'Skiibi ft DJ Nuptune, Falz',
            src:'src/tracks/Skiibii-star-do.mp3',
            img:'src/img/Skiibii.jpg',
            plays:"1,345",
            genre:'Apala',
            playlist:false,
            playing:false,
            paused:null
        }
      ],
      current:'' ,
      audio : new Audio()
    }
  },
  methods:{
    me (){
     console.log("Me")
    },
    play(item, toPlayNext = this.playNext){ 
      
      if(this.tracks[item].paused === true){
        let getIndex = ''
        this.audio.play()
        this.tracks[item].paused === false

        //Setting all other tracks playing property to false so that only the one playing has the pause button 
        this.tracks.forEach((element, index) => {
         
          if(index === item){
            element.playing = true
             getIndex = index
        
          }else{
            element.playing = false
            
          }                                                                           
        });
       toPlayNext (getIndex) // Automatic next 
      }else{
        // Check if the track is playing for the first time, in order not to set the src again if it's not, so the music won't start from the beginning when pause/play is clicked

        this.audio.src= this.tracks[item].src;
        let getIndex = ''
        let i = item
        this.tracks.forEach((element, index) => {
         
          if(index === item){
            element.playing = true
            getIndex = index
          }else{
            element.playing = false
          }                                                                           
        });
        
        this.tracks.forEach((track,index)=>{
          if(item == index){
             this.current =[track,i]
          }
        })
        
        this.audio.play()
        toPlayNext (getIndex)
      }
    },
    
    pause (item, time){
      this.audio.pause()
      this.currentTime = time;
      this.tracks[item].playing = false
      this.tracks[item].paused = true
    },
    playNext (index){
      
      // let nextSongToPlay = index + 1
      
      let lastTrackIndex = this.tracks.length - 1
      

      setInterval(()=>{
      
      //  console.log("Oya")

        if(this.audio.ended === true){
          let nextSongToPlay = index + 1
          // console.log("Ended")
          console.log(`index ${index}`)
          console.log(`nextSongToPlay ${nextSongToPlay}`)
          console.log(`lastTrackIndex ${lastTrackIndex}`)
          
          if(nextSongToPlay > lastTrackIndex){
            return null
          }else{
           this.play(nextSongToPlay)
           
          }
         
           
        }
        return null
      },100)
    },
    addToPlaylist (item){
      this.tracks[item].playlist = true
      
    },

    playlistPlayNext (index){
      let nextSongToPlay = index++
      let lastTrackIndex = this.tracks.length - 1
      setInterval(()=>{
        if(this.audio.ended === true){
          
          if(nextSongToPlay > lastTrackIndex){
            return null
          }else{
            this.tracks.forEach((element, index) => {

            })
            if(nextSongToPlay.playlist){
              this.play(nextSongToPlay)
            }else{
              nextSongToPlay+=1
            }
             
            
          }
        }
      },4000)
    },

    nextSong (item){
      let nextPlay = item+=1
      this.play(nextPlay)
    },
    prevSong (item){
      let prevPlay = item-=1
      this.play(prevPlay)
    },
    setPlaying (current){
     
      this.playing = {
            title:'Billionaire',
            artist:'Teni',
            src:'../teni.mp3',
            img:'../img/teni.jpg',
            plays:"123,456",
            genre:'hip-hop',
            playlist:true,
            playing:false

        };
       console.log(this.playing)
      song = this.audio
    }
  },
  created (){
    this.play(0)
     
    this.current[0].playing = false
  },

  components:{
    Placard,
    Playing,
    Tracks
  }
  
  }
</script>

<style>
*{
  list-style:none;
  text-decoration: none;
}
.top{
  position: fixed;
  top:0;
  left:0;
  right:0;
}
.bottom{
  background: #e3e3e3;
  padding:60px 0 40px 0;
  margin-top: 130px;
}
</style>
