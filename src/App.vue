<template>


  <h1 style="text-decoration:underline">VUE - Reaction Timer</h1>
  <button @click="start" class="play-button" :disabled="isPlaying" >
    Let's Play! 
  </button>
<!--@end is the event emitted by the child component  -->
  <Block v-if="isPlaying" :delay="delay" @end="endGame" > 
  </Block>
  <h3 v-if="showResults">Reaction Time:  {{score}} ms</h3>
  <div class="message" v-if="showResults"> {{message}} </div>

</template>

<script>
import Block from './components/Block.vue';


export default {
  name: 'App',
  components: {Block},
  data(){
    return{
      isPlaying:false,
      delay:null,
      score:null,
      showResults:false,
      message:""
    }
  },
  methods: {
    start(){
      this.delay= 2000 + Math.random() * 5000;
      this.isPlaying=true;
      this.showResults=false;
    },
    endGame(reactionTimer){
      this.score=reactionTimer;
      this.isPlaying=false;
      this.showResults=true;
      
      if(this.score < 900){
        this.message="Unmatchable Reflexes :O";
      }
      else if (this.score > 900 && this.score < 1550){
        this.message="Fastest Reflexes :p ";
      }
      else if(this.score > 1550 && this.score < 2000)
        this.message="Fast Reflexes :))" ;
      else
        this.message="Slow Reflexes :(";

      
    }

  },
  updated(){

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(17, 18, 49);
  margin-top: 60px;
  background: rgb(149, 197, 191);
  border: 2px solid rgb(61, 3, 3);
  width: 100%;
}
.play-button{
  padding: 10px 50px;
  border: 2px solid rgb(34, 36, 128);
  border-radius: 5px;
  color: rgb(253, 253, 253);
  font-weight: bold;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  cursor: pointer;
  margin: 3%;
  background:  #0275d8;
  font-size: 16px
;
}
:disabled{

    background: #d9534f;
    color: rgb(238, 235, 235);
    text-decoration: line-through;
    cursor:not-allowed;
}
.message{
  width: 100%;
  background: #5cb85c;
  font-weight: lighter;
  border: 1px solid rgb(22, 22, 194);
}
</style>
