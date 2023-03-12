<template>
    <div id="info">
        <h2 class="roles-h">ROLES</h2>
        <div>
            <h4>Lorem ipsum, dolor sit amet consectetur adipisicing.</h4>
            <h4>Lorem ipsum dolor sit amet.</h4>
            <h4>Lorem, ipsum dolor sit amet consectetur adipisicing elit.</h4>
            <h4>Lorem ipsum dolor sit amet consectetur.</h4>
        </div>
       <button @click="onStepChanged('QUIZ')">TAKE THE QUIZ</button> 
    </div> 
</template>

<script>
export default {
    data(){
        return {
            
        }
    },
    methods:{
        onStepChanged(step) {
            this.$emit('step-changed', step);
        },
    }
    
}
</script>

<style>
#info{
    height: 80vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 2em 0;
}
.roles-h{
    color: #00ba92;
}
#info h4{
    color: #00ba92;
    margin: .6em 0;
}
#info div{
    margin: 3em auto;
}
#info button{
    width: 200px;
    margin: auto;
}
</style>