<template>
  <div v-if="category" class="category">
    <span>Category: {{ category }}</span>
  </div>
</template>

<script>
export default {
  name: "Category",
  props: {
    category: String,
  },
};
</script>

<style>
.category {
  /* background: pink; */
  padding: 0.25em;
  display: flex;
  align-items: center;
  justify-content: center;
}

.category span {
  text-align: center;
  /* font-size: clamp(0.5em, 100vw, 0.5em); */
}
</style>