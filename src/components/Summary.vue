<template>
  <div class="end-gamebox">
    <div class="end-game">
      <h1>
        {{
          points == trivia.length
            ? "Perfect Score!"
            : points == 0
            ? "Better Luck Next Time"
            : "Well Done!"
        }}
      </h1>
      <p>Your scored {{ points }} / {{ trivia.length }}</p>
      <span>Returning to Main Menu {{ countdown }}s</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Summary",
  props: {
    points: Number,
    countdown: Number,
    trivia: Array,
  },
};
</script>

<style>
.end-gamebox {
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.end-game {
  background: lightgreen;
  border-radius: 0.75em;
  padding: 0 1em;
  height: 30em;
  width: 25em;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}
</style>