<template>
  <div class="question">
    <h2>{{ question }}</h2>
    <ul>
      <li v-for="(score, answer) in answers" :key="answer" v-on:click="selectAnswer($event)">
        <a href="#" class="answer" :data-score="score">
          {{ answer }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.component('Question', {
  name: 'Question',
  props: {
    question: String,
    answers: Object,
    category: String,
    index: Number
  },
  methods: {
    selectAnswer (e) {
      var score = 0
      if (e.target.tagName === 'LI') {
        score = e.target.querySelector('.answer').dataset.score
      } else {
        score = e.target.dataset.score
      }

      var answerData = {
        index: this.index,
        category: this.category,
        score: score
      }
      this.$emit('answer-selected', answerData)
      e.preventDefault()
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.question {
  text-align: center;
  max-width: 500px;
  margin: 0;
  display: none;
}

.question.active {
  display: block;
}

h1 {
  margin: 0;
}

li {
  list-style: none;
  border: 2px solid #eee;
  border-radius: 15px;
  padding: 20px 40px;
  margin-bottom: 15px;
  text-align: center;
  overflow: auto;
  height: auto;
}

.answer {
  color: #006880;
  font-size: 1.1em;
  text-decoration: none;
  word-wrap: break-word;
  overflow: auto;
  height: auto;
  max-width: 400px;
}

li:hover {
  background: #def;
  border: 2px solid #ddf;
  -moz-box-shadow:    3px 3px 3px 3px #eee;
  -webkit-box-shadow: 3px 3px 3px 3px #eee;
  box-shadow:         3px 3px 3px 3px #eee;
}

.answer-category {
  display: none;
}
</style>
