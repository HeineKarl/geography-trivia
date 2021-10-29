<template>
  <div class="body">
    <Question :questionNum="questionNum" :question="question" />
    <Answers
      @setPoint="setPoint"
      @newQuestion="newQuestion"
      @showResult="showResult"
      :trivia="trivia"
      :correct="correct"
      :incorrect="incorrect"
      :answers="answers"
      :timeCounter="timeCounter"
      :viewAnswer="viewAnswer"
    />
  </div>
</template>

<script>
import Question from "./Question.vue";
import Answers from "./Answers.vue";

export default {
  name: "Body",
  props: {
    trivia: Array,
    question: String,
    questionNum: Number,
    answers: Array,
    correct: String,
    incorrect: Array,
    timeCounter: Number,
    viewAnswer: Boolean,
  },
  components: {
    Question,
    Answers,
  },

  methods: {
    setPoint(point) {
      this.$emit("setPoint", point);
    },

    newQuestion(nextQuestion) {
      this.$emit("newQuestion", nextQuestion);
    },

    showResult(nextQuestion) {
      this.$emit("showResult", nextQuestion);
    },
  },
};
</script>

<style>
</style>