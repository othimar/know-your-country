<script>
import StartVue from './components/Start.vue';
import GameVue from './components/Game.vue'
import EndVue from './components/End.vue'


let questions = [
  {
    question:"Quelle est la capitale du Cameroun ?",
    propositions:[
      'Douala',
      'Garoua',
      'Yaoundé',
      'Buea'
    ],
    answer:2//0-3
  },
  {
    question:"Combien de region compte le Cameroun ?",
    propositions:[
      '5',
      '10',
      '250',
      '11'
    ],
    answer:1
  },
  {
    question:"Laquelle de ces couleurs ne figure pas sur le drapeau du Cameroun ?",
    propositions:[
      'Rouge',
      'Vert',
      'Rose Bonbon',
      'Jaun'
    ],
    answer:2
  },{
    question:"Quel le chef lieu de la region du Nord ?",
    propositions:[
      'Garoua',
      'Maroua',
      'Kousseri',
      'Ngaoundéré'
    ],
    answer:0
  },
  {
    question:"Dans quelle ville se trouve le pont sur le Wouri ?",
    propositions:[
      'Douala',
      'Yaoundé',
      'Yagoua',
      'Bamenda'
    ],
    answer:0
  },
]


export default {
  data() {
    return {
      playerName: '',
      gamePhase: 0, //0:start 1:game 2:end

      questions: questions,
      
      currentQuestion:0,

      score: 0
    }
  },

  methods:{
    start(nom){
      this.gamePhase = 1
      this.currentQuestion = 0
      this.score = 0
      this.playerName=nom
    },

    restartGame(){
      this.gamePhase = 0
    },

    nextQuestion(){
      this.currentQuestion++
      if(this.currentQuestion == this.questions.length){
        this.endGame()
      }
    },

    endGame(){
      this.gamePhase = 2
    },
    checkAnswer(id){
      if(id == questions[this.currentQuestion].answer){
        this.score++
        console.log("Correct")
      }else{
        console.log(`${questions[this.currentQuestion].propositions[id]}:False`)
      }
      this.nextQuestion()

    }

  },

  components:{
    StartVue, 
    GameVue,
    EndVue 
  }

}
</script>

<template>
  <StartVue 
    v-if="gamePhase == 0" 
    @onStartGame="start"/>
  
  
  <GameVue 
    v-else-if="gamePhase == 1" 
    :question="this.questions[currentQuestion]" 
    :questionId="this.currentQuestion+1"
    :numberOfQuestions="this.questions.length"
    @Quit="restartGame"
    @Answer="checkAnswer"
    />

  <EndVue v-else 
    :score="this.score" 
    :total="this.questions.length"
    :playerName="this.playerName" 
    @restart="restartGame"/>
  
</template>

