<template>
  <div @click="flipCard">
    <div
      v-bind:style="{backgroundColor: colorFront, color: colorTextFront}"
      v-show="!isToggle"
      class="animated flipInX flashcard"
    >
      <div class="card-content center">
        <p v-bind:style="{fontSize: textSizeFront,fontWeight: 'bold'}">{{front}}</p>
      </div>
      <div class="card-footer">{{footerFront}}</div>
    </div>
    <div
      v-bind:style="{backgroundColor: colorBack, color: colorTextBack}"
      v-show="isToggle"
      class="animated flipInX flashcard"
    >
      <div class="card-content center">
        <p v-bind:style="{fontSize: textSizeBack, fontWeight: 'bold'}">{{back}}</p>
      </div>
      <div class="card-footer">{{footerBack}}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    front: {
      type: String,
      default: "default front"
    },
    back: {
      type: String,
      default: "default back"
    },
    textSizeFront: {
      type: String,
      default: "2em"
    },
    textSizeBack: {
      type: String,
      default: "2em"
    },
    colorTextFront: {
      type: String,
      default: "black"
    },
    colorTextBack: {
      type: String,
      default: "white"
    },
    colorFront: {
      type: String,
      default: "white"
    },
    colorBack: {
      type: String,
      default: "#2ecc71"
    },
    footerFront: {
      type: String,
      default: "Click to show Back"
    },
    footerBack: {
      type: String,
      default: "Click to show Front"
    }
  },
  computed: {
    isToggle() {
      return this.$store.state.cardFlipped; // handled by vuex
    }
  },
  methods: {
    flipCard() {
      this.$store.commit("flipCard"); // handled by vuex
    }
  }
};
</script>

<style scoped>
.center {
  text-align: center;
}
.flashcard {
  cursor: pointer;
  border-radius: 10px;
  margin: 20px;
  padding: 25px;
  box-shadow: 0 0px 10px rgba(0, 0, 0, 0.4);
  text-align: center;
}
.animated {
  animation-duration: 0.75s;
  animation-fill-mode: both;
}
@keyframes flipInX {
  from {
    transform: perspective(400px) rotate3d(1, 0, 0, 90deg);
    animation-timing-function: ease-in;
    opacity: 0;
  }
  40% {
    transform: perspective(400px) rotate3d(1, 0, 0, -10deg);
    animation-timing-function: ease-in;
  }
  60% {
    transform: perspective(400px) rotate3d(1, 0, 0, 10deg);
    opacity: 1;
  }
  80% {
    transform: perspective(400px) rotate3d(1, 0, 0, -5deg);
  }
  to {
    transform: perspective(400px);
  }
}
.flipInX {
  backface-visibility: visible !important;
  animation-name: flipInX;
}
</style>