<template>
  <div class="question-box-container">
    <h1>Question Box</h1>
    {{ currentQuestion.question }}

  
    <hr>
<div class="list-box">
    <p 
    v-for="(answer, index) in answers" 
    :key="index"
    @click="selectAnswer(index)"
    :class="answerClass(index)"
    >
  {{ answer }}
    </p>
</div>
 

    <b-button class="btn"
    v-on:click="submitAnswer"
    :disabled="selectedIndex === null || answered "
    >
    Submit</b-button>
    <b-button class="btn" @click="next">Next</b-button>
    
  </div>
</template>
<script>
import _ from 'lodash'

export default {
  props: {
    currentQuestion: Object,
    next:Function,
    increment:Function
  },
  data: function() {
    return {
      selectedIndex: null,
      correctIndex:null,
      shuffledAnswers:[],
      answered: false
        }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
       answers.push(this.currentQuestion.correct_answer)
       return answers
    }
  },
  watch: {
    currentQuestion:  {
      immediate:true,
      handler() {
        this.selectedIndex = null
        this.answered = false
        this.shuffleAnswers()
      }

    }
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index
      console.log(index)
    },
    submitAnswer() {
      let isCorrect = false
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true
      }

      this.answered = true
      this.increment(isCorrect)
    },
    shuffleAnswers() {
       let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
       //lodash.shuffle
       this.shuffledAnswers = _.shuffle(answers)
       this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    },
    //選択された回答が正しいかどうかでクラス分け
    answerClass(index) {
      let answerClass = ''

      if ( !this.answered && this.selectedIndex === index) {
        answerClass = 'selected'
      }else if (this.answered && this.correctIndex === index) {
        answerClass = 'correct'
      }else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
         answerClass = 'incorrect'
      }

      return answerClass
   
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
.list-box{
  width: 80%;
  margin: 0 auto;
  max-width: 500px;

}

p:hover {
  background-color: rgb(206, 206, 206);
  cursor: pointer;
}
.selected {
  background-color: lightblue;
}
.correct {
  background-color: rgb(50, 245, 50);
}
.incorrect {
  background-color:red;
}
</style>