<template>
  <div class="block" v-if="showClickMeButton" @click="stopTimer">
      <div class="click-me">
          Click
      </div>
  </div>
</template>

<script>
export default {
    props:['delay'],

    data(){
        return{
            showClickMeButton:false,
            timer:null,
            reactionTimer:0,
        }
    },

    methods:{
        startTimer(){
            this.timer=setInterval(()=>{
                this.reactionTimer+=10;  //timing the reaction time in steps of 10 ms
            })
        }, 
        stopTimer(){
            clearInterval(this.timer);
            this.$emit('end', this.reactionTimer);

        }
    },

    //when component is mounted
    mounted(){
        setTimeout(()=> {
            this.showClickMeButton=true;
            this.startTimer()
            
        }, 
        this.delay)
    },

}
</script>

<style>
.block{
    width: 12%;
    height: 150px;
    border-radius: 100%;
    background: #0d366dea;
    
    color:white;
    text-align:center;
    margin: 10px auto;
    margin-bottom: 40px;
}
.click-me{
    padding-top: 43%;
    font-weight: bold;
}
</style>