<template>
  <div id="quiz-results">
    <h1>RESULTS</h1>
    <div v-on:answer-selected="onAnswerSelected($event)">
      <!-- {{ this.topCategory }} -->
      <p class="identity">Your persona is {{ identity }}!</p>
      <p class="summary">{{ summary }}</p>
      <img class="image" :src="image" />
    </div>
    <!-- <code> -->
    <!--   {{ quizAnswers }} -->
    <!--   <hr> -->
    <!--   {{ categoryDetails }} -->
    <!-- </code> -->
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.component('QuizResults', {
  name: 'QuizResults',
  props: [ 'categoryDetails', 'quizAnswers' ],
  data () {
    return {
    }
  },
  computed: {
    identity: function () {
      return this.categoryDetails[this.topCategory].identity
    },
    summary: function () {
      return this.categoryDetails[this.topCategory].summary
    },
    image: function () {
      return this.categoryDetails[this.topCategory].image
    },
    topCategory: function () {
      /*
       * Calculate Results
       */
      var curTop = 0
      var topCat = ''
      console.log('topCat')
      console.log(this.quizAnswers)

      for (var curCat in this.quizAnswers) {
        console.log('curCat: ' + curCat)
        console.log('curTop: ' + curTop)
        console.log(this.quizAnswers[curCat])
        if (this.quizAnswers[curCat] > curTop) {
          curTop = this.quizAnswers[curCat]
          topCat = curCat
        }
      }
      return topCat
    }
  }
})
</script>

<style scoped>
.identity {
  color: blue;
  font-weight: bold;
}
</style>
