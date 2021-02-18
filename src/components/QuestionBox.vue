<template>
  <div class="question-box-container">
    <h1>Question Box</h1>
    {{ currentQuestion.question }}

 <hr clss="my-4">
    <b-button class="btnSubmit">Submit</b-button>
    <b-button class="btnNext">Next</b-button>
  </div>
</template>
<script>
export default {
  props: {
    currentQuestion:Object
  }
}
</script>

<style scoped>

.btnSubmit {
  background-color: white;
  color: black;
  margin-right: 10px;
}

.btnNext {
  background-color: white;
  color: black;
 
}
  
</style>