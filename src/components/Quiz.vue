<script>
import Vue from "vue";
export default {
  name: "Quiz",
  data() {
    return {
      questionIndex: 0,
      userAnswer: "",
      result: null,
      questions: [
        {
          title: "Hangisi backend dilidir ?",
          options: [
            { title: "Php" , correct: true},
            { title: "Html"},
            { title: "Vue Js" },
            { title: "React" },
          ],
        },
         {
          title: "Hangisi frontend dilidir ?",
          options: [
            { title: "Php" },
            { title: "c#" },
            { title: "Vue Js", correct: true},
            { title: "Java" },
          ],
        },
      ],
    };
  },

  created() {
    this.userAnswer = Array(this.questions.length).fill(null);
  },

  methods: {
    next() {
      if (this.questions.length != this.questionIndex) {
        this.questionIndex++;
      }
    },
    prev() {
      if (this.questionIndex > 0) {
        this.questionIndex--;
      }
    },
    selectOption(oIndex) {
      Vue.set(this.userAnswer, this.questionIndex, oIndex);
    },
    finishQuiz() {
      let score = 0;
      for (let i = 0; i < this.questions.length; i++) {
        if (this.questions[i].options[this.userAnswer[i]].correct) {
          score++;
        }
      }
      this.result = score;
    },
  },
};
</script>

<template>
  <div class="card col-md-5">
    <div>
      <button class="btn btn-success col-12" @click="finishQuiz()">
        Sınav Bitir
      </button>
      <h5 class="card-header">{{ questions[questionIndex].title }}</h5>
      <div class="card-body">
        <ul class="list-group">
          <li
            class="list-group-item"
            :class="{ active: userAnswer[questionIndex] == index }"
            v-for="(option, index) in questions[questionIndex].options"
            :key="index"
            @click="selectOption(index)"
          >
            {{ option.title }}
          </li>
        </ul>
        <div class="mt-3">
          <button class="btn btn-danger" @click="prev()">Geri</button>
          <button class="btn btn-primary ms-2" @click="next()">İleri</button>
        </div>
      </div>
    </div>
    <div class="bg-light p-3" v-if="result">
        <h5 class="text-success">Doğru Cevap :  {{result}}</h5>
        <h5 class="text-danger">Yanlış Cevap :  {{questions.length - result}}</h5>
    </div>
  </div>
</template>

<style scoped>
</style>