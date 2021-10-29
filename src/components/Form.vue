<template>
  <div class="form-box">
    <form @submit.prevent="startGame" class="form">
      <div class="header-form">
        <h2>Geography Game</h2>
      </div>

      <div class="numOfQuest input-box">
        <label for="numOfQuest">Number of Question</label>
        <input id="numOfQuest" v-model="numOfQuest" type="number" required />
      </div>

      <div class="numOfTime input-box">
        <label for="numOfTime">Time</label>
        <input id="numOfTime" v-model="numOfTime" type="number" required />
      </div>

      <div class="choiOfDiff input-box">
        <label for="choiOfDiff">Category</label>
        <select v-model="choiOfDiff" id="choiOfCateg" required>
          <option value="Easy">Easy</option>
          <option value="Medium">Medium</option>
          <option value="Hard">Hard</option>
        </select>
      </div>

      <button class="submit-form" type="submit">Start Game</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "Form",
  data: () => ({
    numOfQuest: 10,
    numOfTime: 60,
    choiOfDiff: "Easy",
  }),
  methods: {
    startGame() {
      if (this.numOfQuest < 1 || this.numOfQuest > 50) {
        alert("Please specify Number of Question 1 - 50");
        return;
      }

      if (this.numOfTime < 1) {
        alert("Please specify Time greater than 0");
        return;
      }

      let data = {
        numOfQuest: this.numOfQuest,
        numOfTime: this.numOfTime,
        choiOfDiff: this.choiOfDiff,
      };
      this.$emit("startGame", data);
    },
  },
};
</script>

<style>
.form-box {
  background: #eee;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.form {
  background: rgb(255, 214, 78);
  margin: 0 auto;
  border-radius: 0.75em;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  padding: 0 1em;
  height: 30em;
  /* width: 25em; */
  width: clamp(18em, 80vw, 25em);
  /* font-size: clamp(2em, 5vw, 4em); */

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}

.submit-form {
  padding: 1em 2em;
  background: var(--bg-button-clr--);
  border-radius: 1em;
  font-size: clamp(0.8em, 4.5vw, 1em);
  color: white;
}

.input-box {
  width: 18em;
  /* width: clamp(13em, 60vw, 18em); */
  font-size: clamp(0.8em, 4vw, 1em);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.numOfQuest {
  /* background: pink; */
  width: 18em;
  display: flex;
  align-items: center;
  justify-content: space-between;
  /* flex-direction: column; */
}

.numOfTime {
  /* background: pink; */
  width: 18em;
  display: flex;
  /* flex-direction: column; */
  align-items: center;
  justify-content: space-between;
}
</style>