<template>
  <div id="app">
    <Header :numCorrect="numCorrect"
            :numTottal="numTottal"/>

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox v-if="questions.length" 
                       :currentQuestion="questions[index]"
                       :next="next"
                       :noQuestion="noQuestion"
                       :increment="increment"/>
        </b-col>
      </b-row>
    </b-container>

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
  data(){
    return {
      questions: [],
      index: 0,
      noQuestion: true,
      numCorrect: 0,
      numTottal: 0
    }
  },
  methods: {
    next(){
      if((this.questions.length - 1) === this.index) {  this.noQuestion = false;  }
      else { this.index++; }
    },
    increment(isCorrect){
      if(isCorrect){
        this.numCorrect++;
      }
      this.numTottal++;
    }
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=18&difficulty=medium&type=multiple', {
      method: 'get'
    })
    .then((response) => {
      return response.json();
    })
    .then((jsonData) => {
      this.questions = jsonData.results;
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
