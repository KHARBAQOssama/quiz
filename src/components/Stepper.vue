<template>
  <div class="stepper" id="stepper">
    <div v-for="step in steps" :key="step.name" :class="step.active ? 'step active' : 'step'"><span v-html="step.icon"></span><span>{{step.name}}</span></div>
  </div>
</template>

<script>
export default {
    props : {
        steps:{
            type: Array,
            required : true
        }
    }
}
</script>

<style>
#stepper{
    width: 100%;
    height: 15vh;
    display: flex;
    justify-content: space-around;
    align-items: center;
    position: sticky;
    bottom: 4%;
}
#stepper *{
    transition: all 0.5s;
}
.step{
    border-radius: 25px;
    height: 40px;
    width:  40px;
    border: 2px solid rgb(0, 192, 163);
    color:rgb(0, 192, 163);
    display: flex;
    justify-content: space-around;
    align-items: center;
}
.step.active{
    padding:0 10px;
    background-color: rgb(0,192,163);
    color: white;
    width: 100px;
}
.step > :last-child{
    display: none;
}
.step.active > :last-child{
    display: inline;
}

</style>