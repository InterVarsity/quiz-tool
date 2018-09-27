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
      :quizAnswers="quizAnswers"/>
  </div>
</template>

<script>
import Vue from 'vue'
import Question from '@/components/Question.vue'
import QuizResults from '@/components/QuizResults.vue'

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
        var curTop = 0
        var topCat = ''

        // TODO: replace topCat with flags for above/below threshold
        for (var curCat in this.quizAnswers) {
          if (this.quizAnswers[curCat] > curTop) {
            curTop = this.quizAnswers[curCat]
            topCat = curCat
          }
        }
        this.topCategory = topCat

        this.showResults = true
      }
    },
    loadData: function () {
      var quizData = require('@/quiz.json')

      // Calculate total possible score for each category
      // iterate through questions in category, find high score for each, sum, store
      quizData.maxima = new Proxy({}, handler)
      console.log(quizData.questions)
      quizData.questions.forEach(function (curQuestion) {
        console.log(curQuestion)
        var maxQuestionScore = 0

        // find highest score for question
        for (let curAnswer in curQuestion.answers) {
          console.log(curAnswer)
          if (parseInt(curQuestion.answers[curAnswer]) > maxQuestionScore) {
            maxQuestionScore = parseInt(curQuestion.answers[curAnswer])
          }
        }

        quizData.maxima[curQuestion.category] = maxQuestionScore + quizData.maxima[curQuestion.category]
      })

      this.quizData = quizData
      console.log(this.quizData.maxima)
      console.log(this.quizData.maxima['calling'])
    }
  }
})
</script>

<style scoped>
li {
  list-style: none;
}
</style>
