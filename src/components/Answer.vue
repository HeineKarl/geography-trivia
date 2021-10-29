<template>
  <div class="answer-box">
    <button
      v-if="viewAnswer"
      :class="answer == correct ? 'correct' : 'incorrect'"
      class="answer-btn"
    >
      <span class="answer-text">{{ answer }}</span>
    </button>

    <button v-else class="answer-btn">
      <span class="answer-text">{{ answer }}</span>
    </button>
  </div>
</template>

<script>
export default {
  name: "Answer",
  props: {
    answer: String,
    correct: String,
    incorrect: Array,
    showAnswers: Boolean,
    setAnswer: Function,
    viewAnswer: Boolean,
  },
};
</script>

<style >
.answer-box {
  display: flex;
  align-items: center;
  justify-content: center;
}
.answer-btn {
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
  width: clamp(10em, 40vw, 28em);
  font-size: clamp(0.85em, 3vw, 1.15em);
  height: 8em;
  border-radius: 0.6em;
  cursor: pointer;
  transition: transform 200ms ease;
}

.answer-btn:hover {
  background: rgb(20, 20, 20);
  color: white;
}

.answer-btn:active {
  /* background: rgb(187, 187, 187);
  color: rgb(20, 20, 20); */
  transform: scale(0.9);
}

.incorrect {
  background: rgb(233, 54, 54);
  pointer-events: none;
}

.correct {
  background: rgb(106, 230, 106);
  pointer-events: none;
}
</style>