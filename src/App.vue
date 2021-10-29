<template>
  <div class="App">
    <Header
      v-if="showGame"
      :category="category"
      :difficulty="difficulty"
      :points="points"
      :totalPoints="trivia.length"
      :timeCounter="timeCounter"
      :timesOut="timesOut"
    />
    <Body
      v-if="showGame"
      @setPoint="setPoint"
      @newQuestion="newQuestion"
      @showResult="showResult"
      :trivia="trivia"
      :questionNum="questionNum"
      :question="question"
      :answers="answers"
      :correct="correct"
      :incorrect="incorrect"
      :timeCounter="timeCounter"
      :viewAnswer="viewAnswer"
    />
    <Summary
      v-else-if="endGame"
      :countdown="timeCounter"
      :trivia="trivia"
      :points="points"
    />
    <Form v-else @startGame="startGame" />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Body from "./components/Body.vue";
import Form from "./components/Form.vue";
import Summary from "./components/Summary.vue";

export default {
  name: "App",
  components: { Header, Body, Form, Summary },
  data: () => ({
    showGame: false,
    viewAnswer: false,

    endGame: false,
    timesOut: false,

    trivia: [],
    question: null,
    questionNum: 1,
    answers: null,
    incorrect: [],
    correct: "",
    category: "",
    difficulty: "",
    points: 0,
    timeCounter: 0,
  }),
  // async created() {
  //   let amount = 3;
  //   let difficulty = "easy";
  //   let url = `https://opentdb.com/api.php?amount=${amount}&category=22&difficulty=${difficulty}&type=multiple`;
  //   const response = await fetch(url);
  //   const data = await response.json();
  //   const { incorrect_answers, correct_answer, question, category } = await data
  //     .results[0];

  //   this.trivia = await data.results;
  //   this.incorrect = incorrect_answers;
  //   this.correct = correct_answer;
  //   this.category = category;
  //   this.question = question;

  //   let answers;
  //   answers = incorrect_answers;
  //   answers = [...answers, correct_answer];
  //   answers.sort((a, b) => {
  //     return 0.35 - Math.random();
  //   });

  //   this.answers = answers;
  // },
  methods: {
    async startGame(formData) {
      let amount = formData.numOfQuest;
      let difficultyChoice = formData.choiOfDiff.toLowerCase();
      let url = `https://opentdb.com/api.php?amount=${amount}&category=22&difficulty=${difficultyChoice}&type=multiple`;
      const response = await fetch(url);
      const data = await response.json();
      const { incorrect_answers, correct_answer, question, category } =
        await data.results[0];

      console.log(data);

      this.trivia = await data.results;
      this.incorrect = incorrect_answers;
      this.correct = correct_answer;
      this.category = category;
      this.question = question;
      this.difficulty = formData.choiOfDiff;
      this.questionNum = 1;
      this.points = 0;

      this.timesOut = false;

      let answers;
      answers = incorrect_answers;
      answers = [...answers, correct_answer];
      answers.sort((a, b) => {
        return 0.35 - Math.random();
      });

      this.answers = answers;

      this.timeCounter = formData.numOfTime;
      this.showGame = !this.showGame;

      // Starts the countdown
      let countdown = setInterval(() => {
        this.timeCounter--;

        if (this.timesOut) {
          clearInterval(countdown);
          return;
        }

        // Checking if the game has ended
        if (this.timeCounter === 0) {
          this.timesOut = true;
          this.timeCounter = 5;
          this.viewAnswer = true;

          clearInterval(countdown);

          // Starts the waiting for result
          let waitShowResult = setInterval(() => {
            this.timeCounter--;

            // Checks if the Answers is already shown
            if (this.timeCounter === 0) {
              this.showGame = false;
              this.viewAnswer = false;
              this.endGame = true;

              // Checks if the Results is shown
              if (this.endGame) {
                this.timeCounter = 5;

                clearInterval(waitShowResult);

                // Starts the waiting for Main Menu
                let waitShowMenu = setInterval(() => {
                  this.timeCounter--;

                  // Checks if the Game will be going to the Main Menu
                  if (this.timeCounter === 0) {
                    this.endGame = false;

                    clearInterval(waitShowMenu);
                  }
                }, 1000);
              }
            }
          }, 1000);
        }
      }, 1000);
    },

    setPoint(point) {
      if (point) this.points++;
    },
    newQuestion(nextQuestion) {
      console.log("nextQuestion");
      if (this.trivia.length === nextQuestion) {
        console.log("end");
        this.timeCounter = 0;
        this.endGame = true;
        return;
      }

      let trivia = this.trivia[nextQuestion];
      this.questionNum++;
      this.question = trivia.question;
      this.correct = trivia.correct_answer;
      this.incorrect = trivia.incorrect_answers;

      let answers = this.incorrect;
      answers.push(this.correct);

      answers.sort((a, b) => {
        return 0.35 - Math.random();
      });
      this.answers = answers;
    },
    showResult(nextQuestion) {
      if (this.trivia.length !== nextQuestion) return;

      this.timeCounter = 5;
      this.timesOut = true;

      // Starts the waiting for result
      let waitShowResult = setInterval(() => {
        this.timeCounter--;

        if (this.timeCounter === 0) {
          clearInterval(waitShowResult);
          this.endGame = true;
          this.showGame = false;

          if (this.endGame) {
            this.timeCounter = 5;

            let waitShowMenu = setInterval(() => {
              this.timeCounter--;

              if (this.timeCounter === 0) {
                this.endGame = false;
                clearInterval(waitShowMenu);
              }
            }, 1000);
          }
        }
      }, 1000);
    },
  },
};
</script>


<style>
:root {
  --bg-button-clr--: #1a1a1a;
  --bg-choice-btn--: #1a1a1a;
  --bg-choice-btn-hov--: #eeeeee;
  --bg-timer-btn--: #1a1a1a;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font: 400 1em "Poppins", sans-serif;
}

button {
  font: inherit;
  outline: 0;
  border: 0;
  transition: transform 200ms ease;
  cursor: pointer;
}

button:active {
  transform: scale(0.95);
}

input,
select {
  padding: 0.5em;
  font-size: 1em;
  width: 6em;
  outline: 0;
}

/* .App {
  display: flex;
  align-items: center;
  justify-content: center;
} */

/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
