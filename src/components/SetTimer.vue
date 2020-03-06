<template>
<div id="timer">
    <div class=".container">
    <div class="page-header">
    <h1>RelaxationTimer</h1>
    </div>
    <div id="timersetting">
        <div class="col col-md-12">
        <h3>Set Timer</h3>
        <input  v-model="timerLimit.seconds" class="form-control" type="number" placeholder="Set seconds" min=0 max=150/>
        <input   v-model="timerLimit.minutes"   class="form-control" type="number" placeholder="Set minutes" min=0 max=150/>
        <input   v-model="timerLimit.hours"  class="form-control" type="number" placeholder="Set hours" min=0 max=150/>
        <router-link v-on:click.native="passData()" class="btn" to=/Timerpage>Set Timer</router-link>
        </div>
    </div>
    </div>
</div>
</template>
<script>
import {bus} from '../main';
export default {
    name:'SetTimer',
    data(){
        return{
            timerLimit:{
                'seconds':0,
                'minutes':0,
                'hours':0
            }

        }
    },
    methods:{
        passData:function(){
            bus.$emit('datapassed',this.timerLimit);
        }
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
._setTime{
    display: block;
}
.page-header{
    background-color:blue;
}
#timersetting{
    padding-top:120px;
    padding-bottom:300px;
}
input{
text-align: center;
}
.btn{
    border-style: solid;
    background-color: blue;
    color:white;
    font-weight:bold;
    display: block;
}
</style>