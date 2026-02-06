<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li v-for="(choice, index) in question.choices" :key="choice">
        <label :for="`answer${index}`">
          <input
            :id="`answer${index}`"
            type="radio"
            name="answer"
            :value="choice"
            v-model="answer"
          />
          {{ choice }}
        </label>
      </li>
    </ul>
    <button :disabled="!hasAnswered" @click="emits('answer', answer)">
      Question suivante
    </button>
  </div>
</template>
<script setup>
import { computed, ref } from "vue";

const props = defineProps({
  question: Object,
});
const answer = ref(null);
const emits = defineEmits(["answer"]);
const hasAnswered = computed(() => answer.value !== null);
</script>
<style>
.question button {
  margin-left: 60%;
}
</style>
