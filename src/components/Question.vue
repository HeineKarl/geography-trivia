<template>
  <div v-if="question" class="question-box">
    <p>Question {{ questionNum }}</p>
    <p class="question-text">{{ question }}</p>
  </div>
</template>

<script>
export default {
  name: "Question",
  props: {
    question: String,
    questionNum: Number,
  },
};
</script>

<style>
.question-box {
  /* background: #cacaca; */
  height: 9em;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.question-text {
  text-align: center;
  font-size: clamp(0.8em, 4vw, 1.45em);
  padding: 0 1em;
}
</style>