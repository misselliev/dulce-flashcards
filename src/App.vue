<template>
  <div id="app">
    <div class="score">Score: {{ score }}</div>
    <flashcard :front="question" :back="answer"></flashcard>

    <div v-if="this.$store.state.cardFlipped">
      <button @click="correct">Correct</button>
      <button @click="wrong">Wrong</button>
    </div>
  </div>
</template>

<script>
import flashcard from './components/Flashcard.vue'

export default {
  name: 'App',
  components: {
    flashcard,
  },
  data() {
    return {
      score: 0,
    }
  },
  computed: {
    question () {
      return this.$store.getters.currentQuestion
    },
    answer () {
      return this.$store.getters.currentAnswer
    },
  },
  methods: {
    correct () {
      this.$store.dispatch('correctAnswer')
      this.score++
    },
    wrong () {
      this.$store.dispatch('wrongAnswer')
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
