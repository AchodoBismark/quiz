<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <app-question
        v-if="questionAnswered < questions.length"
        :questions="questions"
        :questionAnswered="questionAnswered"
        @question-answered="questionHasAnswered"
      />
      <app-result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>
    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-show="questionAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import appQuestion from "./components/appQuestion.vue";
import appResult from "./components/appResult.vue";
export default {
  name: "App",
  components: { appQuestion, appResult },
  data() {
    return {
      questionAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: "What is 2 + 2?",
          answers: [
            {
              text: "4",
              is_correct: true,
            },
            {
              text: "3",
              is_correct: false,
            },
            {
              text: "Fish",
              is_correct: false,
            },
            {
              text: "5",
              is_correct: false,
            },
          ],
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: "5",
              is_correct: false,
            },
            {
              text: "7",
              is_correct: false,
            },
            {
              text: "6",
              is_correct: true,
            },
            {
              text: "12",
              is_correct: false,
            },
          ],
        },
        {
          q: "Find the missing letter: C_ke",
          answers: [
            {
              text: "e",
              is_correct: false,
            },
            {
              text: "a",
              is_correct: true,
            },
            {
              text: "i",
              is_correct: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!",
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!",
        },
      ],
    };
  },
  methods: {
    questionHasAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }
      this.questionAnswered++;
    },
    reset() {
      this.questionAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>
