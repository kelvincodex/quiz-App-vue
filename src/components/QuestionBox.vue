<template>
   <div class="container mx-auto w-4/12">
   <div class="mt-5 p-4  border-4 border-sky-500 h-100">
  
      <div class="p-5 items-center">
  {{ currentQuestion.question }}
      </div>
      <hr class="mb-4">
      
      <div  v-for="(answer, i) in answers" :key="i" class="w-4/8 mb-4 text-sm font-medium text-gray-900 bg-white rounded-lg border border-gray-200 dark:bg-gray-700 dark:border-gray-600 dark:text-white">
    <a href="#" @click="selectAnswer(i)" :class="answeredQuestion(i)" aria-current="true" class="block py-2 px-4 w-full text-dark rounded-t-lg border-b border-gray-200 cursor-pointer dark:bg-gray-800 dark:border-gray-600">
        {{ answer }}
    </a>
      </div>

      <div class="flex items-center">
      <button @click.prevent="submitAnswer" :disabled="selectedIndex === null || answered"  class="block mx-2  items-center py-2 px-3 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">submit</button>
      <button @click.prevent="next" class="block mx-2 items-center py-2 px-3 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">next</button>
      </div>
   </div>

</div>
</template>

<script>
import _ from 'lodash'

export default ({
props: {
   currentQuestion:Object,
   next: Function,
   increament: Function
},
data() {
   return {
      selectedIndex: null,
      correctIndex: null,
      shuffledQuestion: [],
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
   currentQuestion: {
      immediate: true,
      handler() {
         this.selectedIndex = null
         this.answered = false
         this.shuffleQuestion()
      }
   }
},
methods:{
  selectAnswer(i) {
   this.selectedIndex = i
   console.log(this.selectedIndex)
  },
  submitAnswer() {
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
         isCorrect = true;
      }
      this.answered = true

      this.increament(isCorrect)
  },
   shuffleQuestion(){
       let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      this.shuffledQuestion = _.shuffle(answers)
      this.correctIndex = this.shuffledQuestion.indexOf(this.currentQuestion.correct_answer)
   },
   answeredQuestion(i) {
      let answeredClass = ''

      if (!this.answered && this.selectedIndex === i) {
            answeredClass = 'bg-blue-300'
      }else if (this.answered && this.correctIndex === i) {
            answeredClass = 'bg-green-200'
      }else if (this.answered && this.selectedIndex === i && this.correctIndex !== i) {
            answeredClass ='bg-red-200'
      }else{
         answeredClass = ''
      }
   return answeredClass
   },
},
mounted() {
   console.log(this.currentQuestion)
}


})

</script>
