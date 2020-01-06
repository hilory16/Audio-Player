<template>
  <div class="container">
      <div id="content">
          <div id="heading">
              <h2>{{this.heading}}</h2>
          </div>

          <div id="body">
              <div id="form">
                  <input type="text" v-model="food">
                  <button v-on:click="addFood">Add Food</button>
              </div>
              <div v-for="food in foods">
                  <ul>
                      <li>{{food.type}} <span>{{food.price}}</span> </li>
                  </ul>
              </div>
               <p v-on:click="play"><i class="fa fa-play"></i></p>
               <p v-on:click="pause"><i class="fa fa-pause"></i></p>
               <p v-on:click="load">load</p>
               <p>{{time}}</p>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    name:'Placard',
    data (){
        return{
            food:"",
            price:"",
            foods:[],
            heading:"Order Your Meal",
            audio : new Audio('../../timi.mp3'),
            time:''
        }
    },
    methods:{
        addFood()  {
            if(this.food==="") return console.log("Field Can't be Empty!!! ");
            const type = this.food;
            const price = this.selectPrice (this.food)
            console.log(price)
            this.foods.push({type,price});
            this.food=""
        },
        selectPrice (item){
            let price = ''
            switch(item){
                case "Salad":
                    price = "#200"
                    break;
                
                case "chicken":
                    price = "#1000"
                    break;
                
                case "rice":
                    price = "#1200"
                    break;
                
                default:
                    price = "n/a"
            }
            return price
        },
        play(){
            this.audio.play()
        },
        pause(){
            
            this.audio.pause()
        },
        load(){
            
            // this.audio.load()
            console.log(this.audio.seekable) 
            
        },
        created (){
            this.time = this.audio.currentTime;
        }

    } 
}
</script>

<style>
    .container{ 
        /* background:#e3e3e3;
        padding:30px 60px; */
    }
</style>