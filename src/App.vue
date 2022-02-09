<template>


<Header
  :numTotal="numTotal"
  :numCorrect="numCorrect"

 />

<QuestionBox
v-if="questions.length"
:currentQuestion ='questions[index]'
:next='next'
:increament="increaments"
 />



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
      questions:[],
      index:0,
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods:{
     next() {
       return this.index ++
     },
     increaments(param) {
        // console.log(param)
        if (param) {
          this.numCorrect++
        }
        this.numTotal++
     }
  },
  mounted() {
  fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple')
        .then(respo => respo.json())
        .then(data => this.questions = data.results)
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
  margin-top: 10px;
}
</style>
