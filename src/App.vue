<template>
  <div id="app">
    <Quiz
      title="Who's your apostle doppelganger?" />
  </div>
</template>

<script>
import Quiz from './components/Quiz.vue'

export default {
  name: 'app',
  components: {
    Quiz
  }
}
</script>

<style>
body {
  background: linear-gradient(0deg, rgba(249,157,28,1) 2%, rgba(245,245,245,1) 40%);
  min-height: 100vh;
  padding: 20px;
}
#app {
  background: #f1fcff;
  border: 1px solid #006880;
  padding: 50px;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 600px;
  min-height: 75%;
  margin-left: auto;
  margin-right: auto;
  -moz-box-shadow:    0px 10px 40px 10px rgba(0, 104, 128, 0.3);
  -webkit-box-shadow: 0px 10px 40px 10px rgba(0, 104, 128, 0.3);
  box-shadow:         0px 10px 40px 10px rgba(0, 104, 128, 0.3);
}
</style>
