<template>
  <div class="container">
    <div v-if="state === 'error'">Impossible de charger le quiz</div>
    <div v-else>
      <Quiz :quiz="quiz" v-if="quiz" />
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import Quiz from "./components/Quiz.vue";
const quiz = ref(null);
const state = ref("loading");
onMounted(() => {
  fetch("/quiz.json")
    .then((r) => {
      if (r.ok) {
        return r.json();
      } else {
        throw new Error("Impossible de récupérer le json");
      }
    })
    .then((data) => {
      quiz.value = data;
      state.value = "idle";
    })
    .catch((e) => {
      state.value = "error";
    });
});
</script>
<style>
.container {
  margin-top: 10%;
  margin-left: 30%;
  border: 2px solid darkblue;
  border-radius: 20px;
  width: 38%;
  padding: 20px;
}
</style>
