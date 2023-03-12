<template>
  <div id="results">
    <h2 class="roles-h">RESULTS</h2>
    <div class="result">
        you have got {{ score }} correct from {{ questions.length }}
    </div>
    <div class="answers">
        <div v-for="(answer,index) in answers" :class="questions[answer.question].correct == answer.chosen ? 'answer' : 'answer incorrect'" :key="index">
            <div class="question">{{ questions[answer.question].question }}</div>
            <div class="choices">
                <div v-for="(choice,inde) in questions[answer.question].choices" :key="inde" class="choice">
                    <div class="feed">
                        <p v-if="questions[answer.question].correct == inde" style="margin-right:auto;">correct answer</p>
                        <p v-if="answer.chosen == inde" style="margin-left:auto;">your answer</p>
                    </div>
                    <div style="color:#00ba92 !important; padding: .2em 0;">{{ choice }}</div>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    props:{
        questions :{
            type: Array,
            required : true,
        },
        answers :{
            type: Array,
            required : true,
        },
    },
    computed:{
        score(){
            let count =0
            this.answers.forEach(answer => {
                if(this.questions[answer.question].correct == answer.chosen) count++
            });
            return count
        }
    }
}
</script>

<style>
#results{
    height: 80vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 2em 0;
}
#results *{
    color:#00ba92;
}
#results h2{
    height: 10vh;
}
.result{
    height: 15vh;
}
.answers{
    height: 55vh;
    overflow-x: scroll;
    width: 450px;
    margin: auto;
    box-shadow: inset 0 0 10px #79797968;
    border-radius: 5px;
}
.answer .choices .choice p{
    font-size: 10px;
    padding: 0 1em;
}
.answer .choices .choice div{
    font-size: 14px;
    color: #00ba92;
}
.answer .choices .choice{
    width: 95%;
    margin: 3px auto;
    padding: 0;
    background-color: white;
    color: #00ba92;
}
.answer{
    background-color: #00ba92;
    padding: 10px 4px;
    border-radius: 5px;
    margin: 1em auto;
}
.answer .question{
    color: white !important;
    font-weight: bold;
    margin-top: 10px ;
}
.answer div{
    color: white !important;
}
.feed{
    display: flex;
}
.choice-content{
    color: #00ba92;
}
.incorrect{
    background-color: #ca4831 !important;
}
</style>