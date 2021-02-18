<template>
  <div id="app">
    <Header></Header>
    <question-box/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=20&category=31&difficulty=medium&type=multiple', {
      method: 'get'
    })
    .then((response) => {
      console.log(response.json())
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
