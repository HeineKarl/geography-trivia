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
  background: lightgreen;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.form {
  margin: 0 auto;
  background: rgb(231, 231, 231);
  border-radius: 0.75em;

  padding: 0 1em;
  height: 30em;
  width: 25em;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}

.submit-form {
  padding: 1em 2em;
  background: var(--bg-button-clr--);
  border-radius: 1em;
  color: white;
}

.input-box {
  width: 18em;
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