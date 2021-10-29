<template>
  <div class="answers-box">
    <Answer
      v-for="answer in answers"
      @click="setAnswer"
      :answer="answer"
      :correct="correct"
      :incorrect="incorrect"
      :viewAnswer="viewAnswer || showAnswers"
    />
  </div>
</template>

<script>
import Answer from "./Answer.vue";

export default {
  name: "Answers",
  props: {
    trivia: Array,
    answers: Array,
    correct: String,
    incorrect: Array,
    timeCounter: Number,
    viewAnswer: Boolean,
  },
  components: { Answer },
  data: () => ({
    showAnswers: false,
    nextQuestion: 0,
  }),

  methods: {
    setAnswer(e) {
      // Restrict the user to click the button several times
      if (this.showAnswers) return;

      // It shows the all answers whether it is correct or not
      // this.$emit("setAnswer", this.viewAnswer);
      this.showAnswers = true;

      // If it is correct, plus point
      if (e.target.textContent === this.correct) this.$emit("setPoint", true);

      // Next Question Number
      this.nextQuestion++;

      // Wait for 3s to the next question
      let next = setInterval(() => {
        this.showAnswers = false;
        this.$emit("newQuestion", this.nextQuestion);
        clearInterval(next);
      }, 1000);

      // Clearing the Interval
      if (this.trivia.length === this.nextQuestion) {
        clearInterval(next);
        this.$emit("showResult", this.nextQuestion);
      }
    },
  },
};
</script>

<style>
.answers-box {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1em;
  flex-wrap: wrap;
}
</style>