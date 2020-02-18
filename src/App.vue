<template>
  <div id="app">
    <h1 class="title">Dulce's React flashcards</h1>
    <div class="score">Score: {{ score }}</div>
    <flashcard :front="question" :back="answer"></flashcard>

    <div v-if="this.$store.state.cardFlipped">
      <button @click="correct">Correct</button>
      <button @click="wrong">Wrong</button>
    </div>
  </div>
</template>

<script>
import flashcard from "./components/Flashcard.vue";

export default {
  name: "App",
  components: {
    flashcard
  },
  data() {
    return {
      score: 0
    };
  },
  computed: {
    question() {
      return this.$store.getters.currentQuestion;
    },
    answer() {
      return this.$store.getters.currentAnswer;
    }
  },
  methods: {
    correct() {
      this.$store.dispatch("correctAnswer");
      this.score++;
    },
    wrong() {
      this.$store.dispatch("wrongAnswer");
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Courgette&display=swap");
html {
  background: url(https://images.unsplash.com/photo-1526280524276-51b1c8a46321?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=967&q=80);
  background-size: cover;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.title {
  font-family: "Courgette", cursive;
  font-size: 2rem;
  color: #ff79c6;
}
</style>
