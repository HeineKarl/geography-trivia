<template>
  <div class="difficulty">
    <span>Difficulty: {{ difficulty }}</span>
  </div>
</template>

<script>
export default {
  name: "Difficulty",
  props: {
    difficulty: String,
  },
};
</script>

<style >
.difficulty {
  /* background: green; */
  padding: 0 0.25em;
}
/* .difficulty {
  width: var(--width);
  height: var(--height);
  display: flex;
  align-items: center;
  justify-content: center;
} */

.difficulty span {
  text-align: center;
  /* font-size: clamp(0.75em, 100vw, 1em); */
}
</style>