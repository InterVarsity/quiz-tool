<template>
  <div id="quiz-container">
    <h1>{{ title }}</h1>
    <ul>
      <li v-for="(curQuestion, index) in this.quizData.questions" :key="index">
        <Question
          :question="curQuestion.title"
          :answers="curQuestion.answers"
          :index="index"
          v-on:answer-selected="onAnswerSelected($event)"
          v-bind:class="{ active: questionIndex == index }" />
      </li>
    </ul>
  </div>
</template>

<script>
import Question from '@/components/Question.vue'
import QuizResults from '@/components/QuizResults.vue'

export default {
  name: 'Quiz',
  components: {
    Question,
    QuizResults
  },
  props: [ 'title' ],
  data () {
    return {
      quizData: {},
      questionIndex: 0
    }
  },
  beforeMount: function () {
    this.loadData()
  },
  mounted: function () {
  },
  methods: {
    onAnswerSelected: function (e) {
      console.log('parent received answer selected')
      this.questionIndex = this.questionIndex + 1
      console.log(e)
    },
    loadData: function () {
      var quizData = require('@/quiz.json')
      this.quizData = quizData
    }
  }
}
</script>

<style scoped>
li {
  list-style: none;
}
</style>
