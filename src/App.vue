<template>
  <div id="app">
    <Header 
    :numCorrect="numCorrect"
    :numTotal="numTotal"

    />
    <QuestionBox v-if="questions.length" 
    :currentQuestion="questions[index]" 
    :next="next" 
    :increment="increment" />
  </div>
</template>

<script>
  import Header from './components/Header.vue';
  import QuestionBox from './components/QuestionBox.vue';

  export default {
    name: 'App',
    components: {
      Header,
      QuestionBox
    },
    data() {
      return {
        questions: [],
        index: 0,
        numCorrect:0,
        numTotal:0
      };
    },
    methods: {
      next() {
        this.index++;
      },
      increment(isCorrect) {
        if(isCorrect){
          this.numCorrect++
        }
        this.numTotal++
      }
    },
    mounted: function() {
      fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', { method: 'get' })
        .then((res) => {
          return res.json();
        })
        .then((data) => {
          console.log(data.results);
          this.questions = data.results;
        });
    }
  };
</script>

<style scoped>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    display: flex;
    align-items: center;
    flex-direction: column;
    /* justify-content: center; */
  }
</style>
