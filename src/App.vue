<template>
  <div id="app">
    <HelloWorld msg="which princess are you"/>
    <Question :question="this.question" :answers="this.answers" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Question from './components/Question.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Question
  },
  data () {
    return {
      question: 'What\'s Up?',
      answers: {
        'Answer1': 'cat1',
        'Answer2': 'cat2',
        'Answer3': 'cat3',
        'Answer4': 'cat4'
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
