<template>
  <div id="app">
    <HelloWorld msg="Vueda o'zimizni sinaymiz test yechamiz " />
    <h1>{{ quiz.title }}</h1>
    <div v-for="(question, index) in quiz.questions" :key="index">
      <div v-show="index === questionIndex">
        <h2>{{ question.text }}</h2>
        <ol>
          <li v-for="response in question.responses" :key="response">
            <label>
              <input type="radio" v-bind:value="response.correct" v-bind:name="index" v-model="userResponses[index]">
              {{ response.text }}
            </label>
          </li>
        </ol>
        <button v-if="questionIndex > 0" v-on:click="prev">
          prev
        </button>
        <button v-on:click="next">
          next
        </button>
      </div>
    </div>
    <div v-show="questionIndex === quiz.questions.length">
      <h2>
        test yechish
      </h2>
      <p>
        Total score: {{ score() }} / {{ quiz.questions.length }}
      </p>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
var quiz = {
  title: "Vueda o'zizni bir sinang",
  questions: [
    {
      text: "Vueni qanday o'rnatadi",
      responses: [
        { text: 'Vue create hello world' },
        { text: 'Vue hello-world' },
        { text: 'Vue create .', correct: true },
      ]
    }, {
      text: "Vueda nechta hooklar bor",
      responses: [
        { text: '6', correct: true },
        { text: '7' },
        { text: '8' },
      ]
    },
    {
      text: "Vue slot nima vazifa bajaradi",
      responses: [
        { text: 'Vue propsni hosil qiladi' },
        { text: 'Vue components xosil qiladi' },
        { text: 'Parent commponentsdan chayldga malumot joylashda ishlatiladi', correct: true },
      ]
    },
    {
      text: "Vueda v-if va v-show farqi nimada",
      responses: [
        { text: "to'g'risi bilmadim" },
        { text: 'v-if bilan v-show birxil ' },
        { text: 'v-if elementni olib tashlaydi v-show esa display none qilib qoyadi', correct: true },
      ]
    },
    {
      text: "Vueda scoped qanday vazifasi bor",
      responses: [
        { text: 'vue scoped css fayni glabal qiladi' },
        { text: 'ochig"i bilmadim' },
        { text: 'Vue scoped css faylni o"sha componetdan boshqasiga sitil otkazmaydi', correct: true },
      ]
    },
  ]
};
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      quiz: quiz,
      questionIndex: 0,
      userResponses: Array(quiz.questions.length).fill(false)
    }
  },
  methods: {
    next: function () {
      this.questionIndex++;
    },
    prev: function () {
      this.questionIndex--;
    },
    score: function () {
      return this.userResponses.filter(function (val) { return val }).length;
    }
  },

}
</script>

<style>
#app {
  width: 1000px;
  margin: 0 auto;
}
</style>
