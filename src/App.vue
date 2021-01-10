<template>
  <div id="app">
    <CompHeader
      :numCorrect="numCorrect"
      :numTotal="numTotal"
      />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="9" offset="2">
              <QuestionsBox
              v-if="questions.length"
              :currentQuestion="questions[index]"
              :next="next"
              :increment="increment"
              />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import CompHeader from './components/CompHeader.vue'
import QuestionsBox from './components/QuestionsBox.vue'

export default {
  name: "app",
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods: {
    next(){
      this.index++
    },
    increment(isCorrect){
      if (isCorrect) {
        this.numCorrect++
      }
        this.numTotal++
    }
  },
  components: {
    CompHeader,
    QuestionsBox
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple',{
      method: 'get'
    })
    .then((response) => {
      return response.json()
    })
    .then((jsonData) => {
      this.questions = jsonData.results
    })
  }
}
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
