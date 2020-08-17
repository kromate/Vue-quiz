<template>
  <div class="card">
    <h1>{{currentQuestion.question}}</h1>
    <hr />
    <p></p>

    <ul>
      <li v-for="(answer, index) in answers" :key="index" @click="selectAnswer(index)" :class="answerClass(index)">{{ answer }}</li>
    </ul>

    <button class="submit" @click="submitAnswer" :disabled="selectedIndex === null || answered">
      Submit
    </button>
    <button class="next" @click="next">
      Next
    </button>
  </div>
</template>

<script>
  // import _ from 'lodash'
  export default {
    name: 'QuestionBox',
    props: {
      currentQuestion: Object,
      next: Function,
      increment: Function
    },
    data() {
      return {
        selectedIndex: null,
        correctIndex: null,
        shuffleAnswers: [],
        answered: false
      };
    },
    methods: {
      answerClass(index) {
        let answerClass = '';

        if (!this.answered && this.selectedIndex === index) {
          answerClass = 'selected';
        } else if (this.answered && this.correctIndex === index) {
          answerClass = 'correct';
        } else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
          answerClass = 'incorrect';
        } else {
          answerClass = '';
        }

        return answerClass;
      },
      submitAnswer() {
        let isCorrect = false;

        if (this.selectedIndex === this.correctIndex) {
          isCorrect = true;
        }
        this.answered = true;

        this.increment(isCorrect);
      },
      selectAnswer(index) {
        console.log(index);
        this.selectedIndex = index;
      },

    },
    watch: {
      currentQuestion: {
        immediate: true,
        handler() {
          this.selectedIndex = null;
          this.answered = false;
        }
      }
    },
    // mounted(){
    //   this.shuffleAnswer()
    // },
    computed: {
      answers() {
        let answer = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];

        return answer;
      }
    }
  };
</script>

<style scoped>
  ul {
    list-style: none;
    display: flex;
    flex-direction: column;
      padding: 40px;
  }
  li {
    background-color: aliceblue;

    outline: 1px solid black;
    padding: 10px;
  }
  li:hover {
    background-color: rgb(87, 111, 133);
    cursor: pointer;
  }
  .selected {
    background-color: lightblue !important;
  }
  .correct {
    background-color: lightgreen;
  }
  .incorrect {
    background-color: rgb(226, 148, 148);
  }
  button {
    border-radius: 5px;
    border: none;
    margin: 3px 5px;
    padding: 10px;
  color: white;
  }
  .next{
    background-color: rgb(38, 38, 110);
  }
  .submit{
    background-color: rgba(25, 77, 25, 0.85);
  }
  template {
    display: block;
  }
  .card {
    background-color: grey;
    width: fill-available;
  }
</style>
