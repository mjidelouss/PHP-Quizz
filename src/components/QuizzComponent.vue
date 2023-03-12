<script setup>
/* eslint-disable */
import { ref, computed } from 'vue'
// import { questions } from "../data.js";
const questions = ref([
  {
	question: 'What is Vue?',
	answer: 0,
	options: [
		'A framework',
		'A library',
		'A type of hat'
	],
	selected: null
  },
  {
	question: 'What is Vuex used for?',
	answer: 2,
	options: [
		'Eating a delicious snack',
		'Viewing things',
		'State management'
	],
	selected: null
  },
  {
	question: 'What is Vue Router?',
	answer: 1,
	options: [
		'An ice cream maker',
		'A routing library for Vue',
		'Burger sauce'
	],
	selected: null
  }
])

const quizCompleted = ref(false)
const currentQuestion = ref(0)
const timer = ref(30)
let timerInterval
const shuffledQuestions = computed(() => questions.value.slice().sort(() => Math.random() - 0.5))

const score = computed(() => {
	let value = 0
	shuffledQuestions.value.map(q => {
		if (q.selected != null && q.answer == q.selected) {
			value += 100
		}
	})
	return value
})
const getCurrentQuestion = computed(() => {
	let question = shuffledQuestions.value[currentQuestion.value]
	question.index = currentQuestion.value
	return question
})
const SetAnswer = (e) => {
	shuffledQuestions.value[currentQuestion.value].selected = e.target.value
	e.target.value = null
}
const NextQuestion = () => {
	if (currentQuestion.value < shuffledQuestions.value.length - 1) {
		currentQuestion.value++
		resetTimer()
		return
	}
	quizCompleted.value = true
}
const startTimer = () => {
	timerInterval = setInterval(() => {
		timer.value--
		if (timer.value < 0) {
			clearInterval(timerInterval)
			timer.value = 0
			NextQuestion()
		}
	}, 1000)
}
const resetTimer = () => {
	clearInterval(timerInterval)
	timer.value = 30
	startTimer()
}

startTimer()
</script>

<template>
    <div>
  <!-- QUIZZ CONTAINER -->
  <div class="container rounded p-3" v-if="!quizCompleted">
        <div class="justify-center flex-column">
          <div id="box">
            <div class="box-item">
              <p id ="progressText" class="box-para fw-bold">
                {{ `Question ❔ ${currentQuestion + 1}/${shuffledQuestions.length}` }}
              </p>
              <div id="progressBar">
                <div id="progressBarFull" :style="{ width: `${((currentQuestion) / shuffledQuestions.length) * 100}%` }"></div>
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
          <h3 id="question" class="mb-4 mt-3">{{ getCurrentQuestion.question }}</h3>
          <div class="options">
				<label 
					v-for="(option, index) in getCurrentQuestion.options" 
					:for="'option' + index" 
					:class="`option ${
						getCurrentQuestion.selected == index 
							? index == getCurrentQuestion.answer 
								? 'correct' 
								: 'wrong'
							: ''
					} ${
						getCurrentQuestion.selected != null &&
						index != getCurrentQuestion.selected
							? 'disabled'
							: ''
					}`">
					<input 
						type="radio" 
						:id="'option' + index" 
						:name="getCurrentQuestion.index" 
						:value="index" 
						v-model="getCurrentQuestion.selected" 
						:disabled="getCurrentQuestion.selected"
						@change="SetAnswer" 
					/>
					<span>{{ option }}</span>
				</label>
			</div>
			
			<button 
                id="qst-btn"
				@click="NextQuestion" 
				:disabled="!getCurrentQuestion.selected">
				{{ 
					getCurrentQuestion.index == questions.length - 1 
						? 'Finish' 
						: getCurrentQuestion.selected == null
							? 'Select an option'
							: 'Next question'
				}}
			</button>
          
        </div>
      </div>
      <section v-if="quizCompleted">
			<h2>You have finished the quiz!</h2>
			<h3>Click on Continue to see your Score</h3>
			<!-- <p>Your score is {{ score }}/{{ questions.length }}</p> -->
		</section>
    </div>
</template>
    
<style lang="scss">
.options {
	margin-bottom: 1rem;
}
.option {
	padding: 1rem;
	display: block;
	background-color: #b394e0;
	margin-bottom: 0.5rem;
	border-radius: 0.5rem;
	cursor: pointer;
}
.option:hover {
	background-color: #96cce1;
}
.option.correct {
	background-color: #2cce7d;
}
.option.wrong {
	background-color: #ff5a5f;
}
.option:last-of-type {
	margin-bottom: 0;
}
.option.disabled {
	opacity: 0.5;
}
.option input {
	display: none;
}
#qst-btn {
	appearance: none;
	outline: none;
	border: none;
	cursor: pointer;
	padding: 0.5rem 1rem;
	background-color: #010905;
	color: #ffffff;
	font-weight: 700;
	text-transform: uppercase;
	font-size: 1.2rem;
	border-radius: 0.5rem;
}
#qst-btn:disabled {
	opacity: 0.5;
}
</style>