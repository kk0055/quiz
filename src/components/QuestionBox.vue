<template>
  <div class="question-box-container">
    <h1>Question Box</h1>
    {{ currentQuestion.question }}

  
    <hr>

    <p 
    v-for="(answer, index) in answers" 
    :key="index"
    @click="selectAnswer(index)"
    >
    {{ answer }}
    </p>

 

    <b-button class="btn">Submit</b-button>
    <b-button class="btn" @click="next">Next</b-button>
    
  </div>
</template>
<script>
export default {
  props: {
    currentQuestion: Object,
    next:Function
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
       answers.push(this.currentQuestion.correct_answer)
       return answers
    }
  },
  methods: {
    selectAnswer(index) {
      console.log(index)
    }
  }
  
}
</script>

<style scoped>

.btn {
  background-color: white;
  color: black;
  margin:10px 10px;
}

.btn:focus {
 outline:none;
 background-color: white;
 color: black;
}
  
</style>