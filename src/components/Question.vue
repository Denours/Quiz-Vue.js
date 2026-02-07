<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li v-for="(choice, index) in randomChoices" :key="choice">
        <Answer
          :id="`answer${index}`"
          :value="choice"
          v-model="answer"
          :disabled="hasAnswered"
          :correctAnswer="question.correct_answer"
        />
      </li>
    </ul>
    <button :disabled="!hasAnswered" @click="emits('answer', answer)">
      Question suivante
    </button>
  </div>
</template>
<script setup>
import { shuffleArray } from "@/functions/array";
import { computed, ref } from "vue";
import Answer from "./Answer.vue";

const props = defineProps({
  question: Object,
});
const answer = ref(null);
const emits = defineEmits(["answer"]);
const hasAnswered = computed(() => answer.value !== null);
const randomChoices = computed(() => {
  return shuffleArray(props.question.choices);
});
</script>
<style>
.question button {
  margin-left: 60%;
}
</style>
