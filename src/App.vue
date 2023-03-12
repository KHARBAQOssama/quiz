<template>
  <div class="container">
    <component 
      :is="activeComponent" 
      :questions="questions"
      :answers="userAnswers"
      :steps="steps"
      :question="[questions[current],questions.length,userAnswers.length]"
      :nextQuestion="onNextQuestion"
      @step-changed="onStepChanged"
      />
    <stepper 
      :steps="steps"
    ></stepper>
  </div>
</template>

<script>
import Stepper from "./components/Stepper.vue";
import Quiz from "./components/Quiz.vue";
import Results from "./components/Results.vue";
import Info from "./components/Info.vue";
import { watch } from "vue";

export default {

  components: {
    Info,
    Stepper,
    Quiz,
    Results,
  },



  data(){
    return {
      steps : [
        {
          name : 'INFO',
          icon : '<i class="bi bi-info-circle-fill"></i>',
          active: true
        },
        {
          name : 'QUIZ',
          icon : '<i class="bi bi-question-circle-fill"></i>',
          active: false
        },
        {
          name : 'RESULTS',
          icon : '<i class="bi bi-check-circle-fill"></i>',
          active: false
        },
        
      ],
      questions : [
        {
          question: 'What is the "v-bind" directive used for in Vue.js?',
          choices: [
            'To bind a JavaScript expression to a DOM element',
            'To define a method on a Vue instance',
            'To define a computed property on a Vue instance',
            'To define a data property on a Vue instance'
          ],
          correct: 0,
          passed: false
        },
        {
          question: 'What is the purpose of the "v-model" directive in Vue.js?',
          choices: [
            'To bind a JavaScript expression to a DOM element',
            'To define a method on a Vue instance',
            'To define a computed property on a Vue instance',
            'To bind form input values to a Vue instance data property'
          ],
          correct: 3,
          passed: false
        },
        {
          question: 'What is the Vue.js lifecycle hook that is called when a component is created?',
          choices: [
            'created',
            'mounted',
            'updated',
            'destroyed'
          ],
          correct: 0,
          passed: false
        },
        {
          question: 'What is the difference between "v-if" and "v-show" in Vue.js?',
          choices: [
            '"v-if" only renders the element if the condition is true, while "v-show" toggles the "display" CSS property',
            '"v-show" only renders the element if the condition is true, while "v-if" toggles the "display" CSS property',
            'There is no difference between "v-if" and "v-show"',
            'Both "v-if" and "v-show" toggle the "display" CSS property'
          ],
          correct: 0,
          passed: false
        },
        {
          question: 'What is the Vue.js directive used to bind to an event?',
          choices: [
            'v-bind',
            'v-model',
            'v-on',
            'v-show'
          ],
          correct: 2,
          passed: false
        },
        {
          question: 'What is the Vue.js component lifecycle hook that is called when a component is destroyed?',
          choices: [
            'created',
            'mounted',
            'updated',
            'destroyed'
          ],
          correct: 3,
          passed: false
        },
        {
          question: 'What is the Vue.js directive used to repeat elements in a list?',
          choices: [
            'v-repeat',
            'v-bind',
            'v-for',
            'v-show'
          ],
          correct: 2,
          passed: false
        },
        {
          question: 'What is the Vue.js feature that allows a parent component to pass data to a child component?',
          choices: [
            'Props',
            'Data',
            'Methods',
            'Computed properties'
          ],
          correct: 0,
          passed: false
        },
        {
          question: 'What is the Vue.js method used to fetch data from an API?',
          choices: [
            'fetch()',
            'get()',
            'post()',
            'axios()'
          ],
          correct: 3,
          passed: false
        },
        {
          question: 'What is the Vue.js feature that allows a component to have its own internal state?',
          choices: [
            'Props',
            'Data',
            'Methods',
            'Computed properties'
          ],
          correct: 1,
          passed: false
        },
        {
          question: 'What is the Vue.js directive used to bind an attribute to a dynamic value?',
          choices: [
            'v-bind',
            'v-model',
            'v-on',
            'v-show'
          ],
          correct: 0,
          passed: false
        }
      ],
      userAnswers : [],
      current: null,
    }
    
  },

  created() {
    this.current = this.currentQuestion();
  },

  computed:{
    activeComponent() {
      const activeIndex = this.steps.findIndex(item => item.active)
      switch (activeIndex) {
        case 0:
          return Info
        case 1:
          return Quiz
        case 2:
          return Results
        default:
          return Info
      }
    }
  },



  methods:{
    onStepChanged(step) {
      this.step = step;
      this.steps.forEach(s => {
        s.active = s.name === this.step;
      });
    },
    currentQuestion(){
      let places = [];
        this.questions.forEach((question,index) =>{
          if(!question.passed){
            places.push(index)
          }
        });
        return places[Math.floor(Math.random() * places.length)];
    },
    onNextQuestion(userAnswer){
      console.log(userAnswer)
      let answer = {
        question: this.current,
        chosen: userAnswer
      };
      
      this.userAnswers.push(answer);
      if(this.userAnswers.length == this.questions.length){
        this.onStepChanged('RESULTS');
      }else{
        this.questions[this.current].passed = true;
        // console.log(this.currentQuestion + 'f');
        this.current = this.currentQuestion();
        console.log(this.current);
      }
    }
  },


  watch:{
    currentQuestionIndex(){
      this.$nextTick(() => {
        console.log(this.currentQuestion);
        this.current = this.currentQuestion;
      });
    }
  }
}
</script>



<style>
.container{
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}
</style>
