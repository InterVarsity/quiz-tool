<template>
  <div class="question">
    <h2>{{ question }}</h2>
    <ul>
      <li v-for="(category, answer) in answers" :key="answer">
        <a href="#" class="answer" v-on:click="selectAnswer($event)">
          {{ answer }}
          <span class="answer-category">{{ category }}</span>
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Question',
  props: {
    question: String,
    answers: Object,
    index: Number
  },
  methods: {
    selectAnswer (e) {
      this.$emit('answer-selected', this.index)
      e.preventDefault()
      console.log(e)
      console.log(e.target)
    }
  }
}
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
  padding: 20px 40px;
  margin-bottom: 15px;
}

.answer {
  text-decoration: none;
  padding: 20px 80px;
  border: 1px solid #eee;
  border-radius: 15px;
}

.answer:hover {
  background: #eef;
  border: 1px solid #ddf;
}

.answer-category {
  display: none;
}
</style>
