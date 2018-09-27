<template>
  <div id="quiz-results">
    <!-- {{ this.topCategory }} -->
    <p class="identity">Your persona is {{ identity }}!</p>
    <p class="summary">{{ summary }}</p>
    <img class="image" :src="image" />
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
  props: [ 'categoryDetails', 'topCategory', 'quizAnswers' ],
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
      return '/img/' + this.categoryDetails[this.topCategory].image
    }
  }
})
</script>

<style scoped>
#quiz-results {
  font-size: 1.4em;
  background: #eef;
  padding: 30px;
  border-radius: 15px;
}

.identity {
  color: blue;
  font-weight: bold;
}

.image {
  width: 400px;
}
</style>
