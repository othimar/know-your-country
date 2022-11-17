<script>
 
 export default{
    props:{
        question:Object,
        questionId:Number,
        numberOfQuestions:Number
    },

    data(){
        return {

        }
    },
    
    methods:{
        onQuit(){
            this.$emit('Quit')
        },
        onAnswer(id){
            this.$emit('Answer', id)
        }

    }
 }
</script>

<template>
    <header>
      <div>Question {{questionId}}/{{numberOfQuestions}}</div>
      <button class="quit" @click="onQuit()">Quitter</button>
    </header>
    
    <h2 class="question">{{question.question}}</h2>

    <div class="propositions">
      <button v-for="i in [0,1,2,3]" class="choice" @click="onAnswer(i)">{{question.propositions[i]}}</button>
    </div>
</template>