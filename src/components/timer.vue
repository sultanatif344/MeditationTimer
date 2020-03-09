<template>
<div id="timer">
    <div class=".container">
    <div class="page-header">
    <h1>RelaxationTimer</h1>
    </div>
    <div id="timerview">
        <div class=".container">

        <div class="col col-md-12">

        <h3>{{this.hours}}:{{this.minutes}}:{{this.seconds}}</h3>
        <button v-on:click="TimerStart()" class="btn">Start</button>
        <button v-on:click="PauseTimer()" class="btn">Pause</button>
        <router-link class="btn" to="/" v-on:click.native="PauseTimer()">Back</router-link>
        </div>
        </div>
    </div>
    </div>
</div>
</template>
<script>
import {bus} from '../main';
export default {
    name:'timer',
    data(){
        //the timerstop variable which stores the id of the set interval
        let intervalID=undefined



        return{
            //the seconds, minutes and hours of the timer
             seconds:0,
             minutes:0,
             hours:0,
            }
        },




        methods:{
            //the Function which starts the interval
            TimerStart:function(){
                this.intervalID=setInterval(this.CountDown,1000);
            },


            //the function which pauses the interval
            PauseTimer:function(){
                clearInterval(this.intervalID);
            },


            /*
            The function which ends the timer
            to be called when a condition is met
            in this case when the seconds, minutes and hours passed
            from the Set Timer component in the timerLimit object are equal to the minutes
            hours and seconds in this component 
            */


            /*The main countdown function which counts down the timer*/
            CountDown:function(){
                if(this.seconds>0){
                    this.seconds-=1;
                    if(this.minutes>0&&this.seconds<=0){
                        this.seconds=60;
                        this.minutes-=1;
                        if(this.hours>0&&this.minutes<=0){
                            this.minutes=60;
                            this.hours-=1
                        }
                    }
                }
                else if(this.minutes>0){
                    this.minutes-=1;
                    if(this.minutes>=0&&this.seconds<=0){
                        this.seconds=60;
                        this.seconds-=1;
                        if(this.hours>0&&this.minutes<=0){
                            this.minutes=60;
                            this.hours-=1
                        }
                    }
                }
                else if(this.hours>0){
                this.hours-=1;
                if(this.hours>=0&&this.minutes<=0){
                    this.minutes=60;
                    this.minutes-=1;
                    if(this.minutes>=0&&this.seconds<=0){
                        this.seconds=60;
                        this.seconds-=1;
                    }
                }
                }
                else if(this.seconds<=0&&this.minutes<=0&&this.hours<=0){
                    var audio=new Audio("alarm.mp3");
                    audio.play();
                }
            }
    },




    created(){
        this.TimerStart();

        /*This is catching the event and the values passed from the event bus from the 
            set Timer components*/
          bus.$on('datapassed',(data)=>{
              /*the start of the mess*/
                    this.seconds=data.seconds;
                    this.minutes=data.minutes;
                    this.hours=data.hours;
                 /*the end of the mess*/   
                })
    }
}
</script>
<style scoped>
#timer{
    background-color:black;
    font-family:Arial,Helvetica,sans-serif;
    font-weight:bold;
}
h1,h2,h3,h4,h5{
color:white;
}
.page-header{
    background-color:blue;
}
#timerview{
    padding-top:120px;
    padding-bottom:400px;
}
.btn{
    border-style: solid;
    border-color: black;
    background-color: blue;
    color:white;
    font-weight:bold;
}
</style>