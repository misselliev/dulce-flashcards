<template>
  <div class="flashcard" @click="flipCard">
    <div v-show="!isToggle">
      <div class="card-content center">
        <p>{{ front }}</p>
      </div>
    </div>
    <div v-show="isToggle">
      <div class="card-content center">
        <p>{{ back }}</p>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    front: {
      type: String,
      default: 'default front',
    },
    back: {
      type: String,
      default: 'default back',
    },
  },
  computed: {
    isToggle () {
      return this.$store.state.cardFlipped
    },
  },
  methods: {
    flipCard () {
      this.$store.commit('flipCard')
    },
  },
}
</script>
<style>
.flashcard {
  border: 1px black;
  border-style: solid;
  padding: 10px;
  margin: 10px;
}
</style>