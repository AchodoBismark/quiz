<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width:  `${(questionAnswered / questions.length) * 100}%` }"
      ></div>
      <div class="status">
        {{ questionAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
     <transition-group name="fade">
    <div
      class="single-question"
      v-for="(question, qi) in questions"
      :key="question.q"
      v-show="questionAnswered === qi"
    >
      <div class="question">{{ question.q }}</div>
      <div
        class="answers"
        v-for="answer in question.answers"
        :key="answer.text"
        @click.prevent="selectAnswer(answer.is_correct)"
      >
        <div class="answer">{{ answer.text }}</div>
      </div>
    </div>
     </transition-group>
  </div>
</template>

<script>
export default {
  props: ["questions", "questionAnswered"],
  emits: ["question-answered"],
  methods: {
    selectAnswer(is_correct) {
      this.$emit("question-answered", is_correct);
    },
  },
};
</script>
