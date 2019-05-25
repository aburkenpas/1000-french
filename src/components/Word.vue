<template>
  <div class="word">
    <div>{{ rank }}:</div>
    <div class="french-word">{{ frenchWord }}:</div>
    <div class="english-word-input">
      <input
        v-if="!answered"
        class="english-word"
        :class="{ shake: answerWrong }"
        type="text"
        name="english-word"
        :ref="rank"
        v-model="userAnswer"
        @keydown.tab="sumbitAnswer"
      />
      <transition name="slide-fade" mode="out-in">
        <div
          class="correctAnswer"
          :class="{ wrong: answerWrong }"
          v-if="answered"
        >
          {{ englishWord }}
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Word',
  props: {
    frenchWord: {
      type: String
    },
    englishWord: {
      type: String
    },
    rank: {
      type: Number
    }
  },
  data: function() {
    return {
      answered: false,
      answerWrong: false,
      userAnswer: ''
    }
  },
  methods: {
    sumbitAnswer: function() {
      if (this.englishWord.toLowerCase() === this.userAnswer.toLowerCase()) {
        this.answered = true
      } else {
        this.answered = true
        this.answerWrong = true
        // setTimeout(() => (this.answerWrong = false), 1000);
      }
    },
    showAnswer: function() {
      this.answered = true
    }
  }
}
</script>

<style lang="scss">
.word {
  display: flex;
  align-items: center;
  width: 100%;
}

.english-word {
  background: none;
  font-size: 1.8rem;
  border: none;
  border-bottom: 0.1rem solid #388aed;
  outline: none;
  padding: 1rem 0.75rem;
  font-family: 'IM Fell French Canon', serif;
  color: #222;
}
.correctAnswer {
  padding: 1rem 0.75rem;
  color: #222;
  box-sizing: border-box;
}

.french-word,
.english-word-input {
  padding: 0 1rem;
}

.french-word {
  width: 15rem;
  font-size: 1.8rem;
  text-align: right;
}

.english-word-input {
  width: 100%;
  padding: 0 1rem;
}

.english-word {
  width: 100%;
}

.slide-fade-enter-active {
  transition: all 0.3s ease;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active for <2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}

.wrong {
  -webkit-animation-name: shake;
  animation-name: shake;
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
  color: red;
}

@-webkit-keyframes shake {
  from,
  to {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }

  10%,
  30%,
  50%,
  70%,
  90% {
    -webkit-transform: translate3d(-10px, 0, 0);
    transform: translate3d(-10px, 0, 0);
  }

  20%,
  40%,
  60%,
  80% {
    -webkit-transform: translate3d(10px, 0, 0);
    transform: translate3d(10px, 0, 0);
  }
}

@keyframes shake {
  from,
  to {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }

  10%,
  30%,
  50%,
  70%,
  90% {
    -webkit-transform: translate3d(-10px, 0, 0);
    transform: translate3d(-10px, 0, 0);
  }

  20%,
  40%,
  60%,
  80% {
    -webkit-transform: translate3d(10px, 0, 0);
    transform: translate3d(10px, 0, 0);
  }
}
</style>
