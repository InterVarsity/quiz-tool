<template>
  <div class="question">
    <h2>{{ question }}</h2>
    <ul>
      <li v-for="answer in shuffledAnswers()" :key="answer" v-on:click="selectAnswer($event)">
        <a href="#" class="answer" :data-score="answers[answer]">
          {{ answer }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
import Vue from 'vue'
var shuffle = require('knuth-shuffle').knuthShuffle

export default Vue.component('Question', {
  name: 'Question',
  props: {
    question: String,
    answers: Object,
    category: String,
    index: Number
  },
  methods: {
    shuffledAnswers () {
      return shuffle(Object.keys(this.answers))
    },
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
  border: 2px solid rgba(0,104,128,0.5);
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
  border: 2px solid #006880;
  -moz-box-shadow:    0px 5px 10px -5px #006880;
  -webkit-box-shadow: 0px 5px 10px -5px #006880;
  box-shadow:         0px 5px 10px -5px #006880;
}

.answer-category {
  display: none;
}
</style>
