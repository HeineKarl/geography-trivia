<template>
  <div v-if="totalPoints" class="points">
    <span>Points: {{ points }} | {{ totalPoints }}</span>
  </div>
</template>

<script>
export default {
  name: "Points",
  props: {
    points: {
      type: Number,
      default: 0,
    },
    totalPoints: Number,
  },
};
</script>

<style>
.points {
  /* background: green; */
  width: var(--width);
  height: var(--height);
  display: flex;
  align-items: center;
  justify-content: flex-end;
}

.points span {
  text-align: end;
}
</style>