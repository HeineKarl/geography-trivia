<template>
  <div v-if="timesOut" class="result-timer">
    <span class="time-count">Showing Results</span>
    <span class="time-count">{{ timeCounter }}s</span>
  </div>
  <div v-else-if="timeCounter" class="time-container">
    <span class="time-count">{{ timeCounter }}</span>
  </div>
</template>

<script>
export default {
  name: "TimeKeeper",
  props: {
    timeCounter: Number,
    timesOut: Boolean,
  },
};
</script>

<style>
.time-container {
  --area-box: clamp(1em, 10vw, 5em);
  background-color: #1a1a1a;
  color: white;
  width: var(--area-box);
  height: var(--area-box);

  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.result-timer {
  --width-box: clamp(12em, 10vw, 15em);
  --height-box: clamp(4em, 10vw, 5em);
  background-color: #1a1a1a;
  border-radius: 0.5em;
  width: var(--width-box);
  height: var(--height-box);

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.time-container span,
.result-timer span {
  color: white;
}
</style>
