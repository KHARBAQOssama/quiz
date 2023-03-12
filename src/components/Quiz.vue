<template>
  <div id="quiz">
      <div class="progress-bar">
        <div class="progress-fill" :style="progressWidth">{{ progress }}</div>
      </div>
     <h3>{{question[0].question}}</h3>
    <div class="choices">
      <div class="choice" :disabled="isDisabled" v-for="(choice,index) in question[0].choices" :value="index" :key="index" @click="click($event)">{{ choice }}</div>
    </div>
  </div> 
</template>

<script>
export default {
  props:{
    question :{
      type: Array,
      required : true,
    },
    nextQuestion : Function,
  },
  data(){
    return {
      isDisabled:false,
    }
  },

  computed:{
    progress(){
      return (((this.question[2])/ this.question[1]) * 100).toFixed(0)+'%'
    },
    progressWidth() {
      return 'width: '+this.progress+';';
    }
  },
  methods:{
    click(event){
      if (!this.isDisabled) {

        this.isDisabled = true;

        let value = event.currentTarget.getAttribute('value');
        if(value == this.question[0].correct){
          event.currentTarget.classList.add('correct');
        }else{  
          event.currentTarget.classList.add('wrong');
        }
        console.log(this.progress);
        setTimeout(() => {
          this.nextQuestion(value);
          this.isDisabled = false;

          document.querySelectorAll('.choice').forEach(item=>{
            item.classList.remove('correct');
            item.classList.remove('wrong');
          })
        }, 1500)

      }
      
    }
  }

}
</script>


<style>
#quiz{
    height: 80vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 2em 0;
}
.progress-bar{
  margin: 1em auto;
  width: 400px;
  height: 25px;
  border: 2px solid #00ba92;
  border-radius: 3px;
}
.progress-fill{
  height: 100%;
  color: white;
  background-color: #00ba92;
  width: 0%;
  transition: all .5s ease;
}

#quiz h3{
  color: #00ba925d;
  text-transform: uppercase;
  -webkit-text-stroke: 1px #00ba92;
}
.choice{
  width: 450px;
  margin: .6em auto;
  border: 2px solid #00ba92;
  color: #00ba92;
  padding: .5em 0;
  border-radius: 10px;
  cursor: pointer;
  transition: all .4s ease;
}
.wrong{
  background-color: #d93e22;
  border: 2px solid #d93e22;
}
.correct{
  background-color: #00ba92;
}
.wrong,.correct{
  color: white;
}
.choices{
  margin: 1em 0;
}
</style>