<template>
  <div class="header">
    <div class="header-information">
      <!-- <Category :category="category" /> -->
      <Difficulty :difficulty="difficulty" />
    </div>
    <TimeKeeper :timesOut="timesOut" :timeCounter="timeCounter" />
    <Points :points="points" :totalPoints="totalPoints" />
  </div>
</template>

<script>
import Category from "./Category.vue";
import Difficulty from "./Difficulty.vue";
import TimeKeeper from "./TimeKeeper.vue";
import Points from "./Points.vue";

export default {
  name: "Header",
  props: {
    category: String,
    difficulty: String,
    timeCounter: Number,
    points: Number,
    totalPoints: Number,
    timesOut: Boolean,
  },
  components: { Category, Difficulty, TimeKeeper, Points },
  methods: {
    setGame(timeCounter) {
      this.$emit("setGame", timeCounter);
    },
  },
};
</script>

<style>
.header {
  --width: clamp(10.75em, 5vw, 14em);
  --height: 4.5em;
  background: rgb(255, 214, 78);
  height: 15vh;
  padding: 0 clamp(2em, 5vw, 4em);
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: clamp(0.65em, 3vw, 1em);
}

.header-information {
  /* background: green; */
  /* width: 14em; */
  width: var(--width);
  height: var(--height);
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
}
</style>