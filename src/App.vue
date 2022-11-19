<script>
import StartVue from './components/Start.vue';
import GameVue from './components/Game.vue'
import EndVue from './components/End.vue'
import { questions } from './data/questions';


export default {
  components: {
    StartVue,
    GameVue,
    EndVue
  },
  data() {
    return {
      playerName: '',
      gamePhase: 0, //0:start 1:game 2:end

      questions: questions,

      currentQuestion: 0,

      score: 0
    }
  },

  methods: {
    start(nom) {
      this.gamePhase = 1
      this.currentQuestion = 0
      this.score = 0
      this.playerName = nom
    },

    restartGame() {
      this.gamePhase = 0
    },

    nextQuestion() {
      this.currentQuestion++
      if (this.currentQuestion == this.questions.length) {
        this.endGame()
      }
    },

    endGame() {
      this.gamePhase = 2
    },
    checkAnswer(id) {
      if (id == questions[this.currentQuestion].answer) {
        this.score++
        console.log("Correct")
      } else {
        console.log(`${questions[this.currentQuestion].propositions[id]}:False`)
      }
      this.nextQuestion()

    }

  },

}

</script>

<template>
  <StartVue v-if="gamePhase == 0" @onStartGame="start" />

  <GameVue v-else-if="gamePhase == 1" :question="this.questions[currentQuestion]" :questionId="this.currentQuestion + 1"
    :numberOfQuestions="this.questions.length" @quit="restartGame" @answer="checkAnswer" />

  <EndVue v-else :score="this.score" :total="this.questions.length" :playerName="this.playerName"
    @restart="restartGame" />

</template>
