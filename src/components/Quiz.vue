<template>
  <div id="quiz-container">
    <h1>{{ title }}</h1>
    <ul>
      <li v-for="(curQuestion, index) in this.quizData.questions" :key="index">
        <Question
          :question="curQuestion.title"
          :answers="curQuestion.answers"
          :category="curQuestion.category"
          :index="index"
          v-on:answer-selected="onAnswerSelected($event)"
          v-bind:class="{ active: questionIndex == index }" />
      </li>
    </ul>
    <QuizResults
      v-if="showResults"
      :categoryDetails="this.quizData.results"
      :topCategory="topCategory"
      :highCats="highCats"
      :quizAnswers="quizAnswers"/>
  </div>
</template>

<script>
import Vue from 'vue'
import Question from '@/components/Question.vue'
import QuizResults from '@/components/QuizResults.vue'

var shuffle = require('knuth-shuffle').knuthShuffle
var handler = {
  get: function (target, name) {
    return target.hasOwnProperty(name) ? target[name] : 0
  },
  has: function (target, prop) {
    if (prop === 'a') { return true }
    return false
  }
}

var Counter = new Proxy({}, handler)

export default Vue.component('Quiz', {
  name: 'Quiz',
  components: {
    Question,
    QuizResults
  },
  props: [ 'title' ],
  data () {
    return {
      quizData: {},
      questionIndex: 0,
      showResults: false,
      topCategory: '',
      highCats: [],
      quizAnswers: Counter
    }
  },
  beforeMount: function () {
    this.loadData()
  },
  mounted: function () {
  },
  methods: {
    onAnswerSelected: function (e) {
      /*
       * Iterate Questions
       */
      this.questionIndex = this.questionIndex + 1
      // Each answer adds its point value to the category's total score
      this.quizAnswers[e.category] = this.quizAnswers[e.category] + parseInt(e.score)

      // Last Question answered
      if (this.questionIndex >= this.quizData.questions.length) {
        // Calculate Results
        var highCats = [] // high is defined as >= 75% of max

        // TODO: replace topCat with flags for above/below threshold
        for (var curCat in this.quizAnswers) {
          if (this.quizAnswers[curCat] >= (this.quizData.maxima[curCat] * 0.75)) {
            highCats.push(curCat)
          }
        }
        this.highCats = highCats.sort()
        this.topCategory = highCats.join('+')
        console.log(this.topCategory)

        this.showResults = true
      }
    },
    loadData: function () {
      var quizData = require('@/quiz.json')

      // Calculate total possible score for each category
      // iterate through questions in category, find high score for each, sum, store
      quizData.maxima = new Proxy({}, handler)
      quizData.questions.forEach(function (curQuestion) {
        var maxQuestionScore = 0

        // find highest score for question
        for (let curAnswer in curQuestion.answers) {
          if (parseInt(curQuestion.answers[curAnswer]) > maxQuestionScore) {
            maxQuestionScore = parseInt(curQuestion.answers[curAnswer])
          }
        }

        // accumulate values for question categories
        quizData.maxima[curQuestion.category] = maxQuestionScore + quizData.maxima[curQuestion.category]

        // randomize answer order
        shuffle(curQuestion.answers)
      })

      // randomize the order of the questions
      shuffle(quizData.questions)

      this.quizData = quizData
    }
  }
})
</script>

<style scoped>
li {
  list-style: none;
}
</style>
