<template>
  <v-stepper v-model="e1">
    <v-stepper-header>
      <v-stepper-step :complete="e1 > 1" step="📜">RULES</v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step :complete="e1 > 2" step="⏳">QUIZ</v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step step="🎯">SCORE</v-stepper-step>
    </v-stepper-header>

    <v-stepper-items>
      <v-stepper-content step="1">
        <v-card
          class="mb-12"
          color="light-blue lighten-5"
          height="450px"
        >
        <h1 class="display-2 lh-1 text-center" style="margin-top: 2rem; color: black;">PHP Knowledge Test</h1>
        <div class="mt-4" id="container">
            <div class="ms-4" id="">
                  <h2 class="text-center fw-bold text-black mt-2">RULES</h2>
                  <h5 class="text-black text-center fw-bold mt-2">💡 The contestant have to answer 12 Questions in PHP.</h5>
                  <h5 class="text-black text-center fw-bold">💡 Each question has a time limit of 30 seconds</h5>
                  <h5 class="text-black text-center fw-bold">💡 With each correct question you get points.</h5>
                  <h5 class="text-center text-black fw-bold mt-2">  😁😁 Good Luck 😁😁</h5>
            </div>
        <img id="quiz" style="margin-left: 20rem;" src="../assets/quizz.png" alt="" height="410" width="520">
        </div>
      </v-card>

        <v-btn
          color="primary"
          @click="e1 = 2"
        >
          Continue
        </v-btn>

        <v-btn text>Cancel</v-btn>
      </v-stepper-content>

      <v-stepper-content step="2">
        <v-card
          class="mb-12"
          color="grey lighten-1"
          height="480px"
        >
        <div class="d-flex justify-content-center">
        <v-btn
      class="ma-2 p-4"
      color="info"
      v-if="showButton" @click="hideButton()"
    >
    <span>Start</span>
    </v-btn>
</div>
  <!-- QUIZZ CONTAINER -->
  <div v-if="!showButton" class="container rounded p-3">
        <div class="justify-center flex-column">
          <div id="box">
            <div class="box-item">
              <p id ="progressText" class="box-para fw-bold">
                Question ❔
              </p>
              <div id="progressBar">
                <div id="progressBarFull"></div>
              </div>
            </div>
            <div class="box-item">
              <p class="box-para fw-bold">Timer ⏳</p>
              <h1 class="box-text" id="timer">{{ timer }}</h1>
            </div>
            <div class="box-item">
              <p class="box-para fw-bold">
                Score 🎯
              </p>
              <h1 class="box-text" id="score">{{ score }}</h1>
            </div>
          </div>
          <h3 id="question" class="mb-4 mt-3">{{  }}</h3>
          <div class="option-container">
            <p class="option-letter">A</p>
            <p class="option-text" id="option1" data-correct="false">{{  }}</p>
          </div>
          <div class="option-container">
            <p class="option-letter">B</p>
            <p class="option-text" id="option2" data-correct="false">{{  }}</p>
          </div>
          <div class="option-container">
            <p class="option-letter">C</p>
            <p class="option-text" id="option3" data-correct="false">{{ }}</p>
          </div>
          <div class="option-container">
            <p class="option-letter">D</p>
            <p class="option-text" id="option4" data-correct="false">{{  }}</p>
          </div>
        </div>
      </div>
      </v-card>

        <v-btn
          color="primary"
          @click="e1 = 3"
        >
          Continue
        </v-btn>

        <v-btn text>Cancel</v-btn>
      </v-stepper-content>

      <v-stepper-content step="3">
        <v-card
          class="mb-12"
          color="grey lighten-1"
          height="200px"
        ></v-card>

        <v-btn
          color="primary"
          @click="e1 = 1"
        >
          Continue
        </v-btn>

        <v-btn text>Cancel</v-btn>
      </v-stepper-content>
    </v-stepper-items>
  </v-stepper>
</template>

<script>
import { questions } from "../data.js";

  export default {
    data () {
      return {
        e1: 1,
        showButton: true,
        shuffledQuestions: [],
        questionIndex: 0,
        optionsHidden: [],
        score: 0,
        questionCounter: 0,
        countdown: 30,
        correctQuestionsCounter: 0,
        incorrectQuestionsCounter: 0,
        MAX_QUESTIONS: questions.length,
        intervalId: null,
      }
    },
    methods: {
    hideButton() {
      this.showButton = false;
    },
    shuffleArray(array) {
      return array.sort(() => Math.random() - 0.5);
    },
    initTest() {
      this.$nextTick(() => {
        this.optionsHidden = new Array(this.shuffledQuestions[this.questionIndex].options.length).fill(true);
        this.optionsHidden.forEach((_, index) => {
          this.$set(this.optionsHidden, index, false);
        });
      });
    },
    startCountdown() {
      this.timer = setInterval(() => {
        if (this.countdown <= 0) {
          clearInterval(this.timer);
          this.timer = null;
          this.incorrectQuestionsCounter++;
          this.goToNextQuestion();
        } else {
          this.countdown--;
        }
      }, 1000);
    },
    goToNextQuestion() {
      this.questionCounter++;
      if (this.questionCounter >= this.MAX_QUESTIONS) {
        sessionStorage.setItem("score", this.score);
        sessionStorage.setItem("correct", this.correctQuestionsCounter);
        sessionStorage.setItem("incorrect", this.incorrectQuestionsCounter);
        if (this.correctQuestionsCounter < this.MAX_QUESTIONS / 2) sessionStorage.setItem("performance", "Bad");
        if (this.correctQuestionsCounter === this.MAX_QUESTIONS / 2) sessionStorage.setItem("performance", "Average");
        if (this.correctQuestionsCounter > this.MAX_QUESTIONS / 2) sessionStorage.setItem("performance", "Good");
        if (this.correctQuestionsCounter === this.MAX_QUESTIONS) sessionStorage.setItem("performance", "Perfect");
        // this.$router.push("/score");
        return;
      }
      this.countdown = 30;
      this.progressBarWidth = `${(this.questionCounter / this.MAX_QUESTIONS) * 100}%`;
      this.startCountdown();
      this.questionIndex++;
      this.initTest();
    },
  }
  }
</script>

<style lang="scss">
#container {
  display: flex;
  flex-direction: row;
  align-items: center;
}

h1, p {
  margin-right: 20px;
}

#quiz {
  float: right;
}
</style>