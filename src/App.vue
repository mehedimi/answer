<template>
  <div id="app">
    <Question/>
  </div>
</template>

<script>
import Question from './components/Question.vue'

export default {
  name: 'app',
  components: {
    Question
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Ubuntu&display=swap');

  #app {
    font-family: 'Ubuntu', sans-serif;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
