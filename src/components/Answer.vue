<template>
  <label :for="id" :class="classes">
    <input
      :id="id"
      type="radio"
      name="answer"
      :value="value"
      v-model="model"
      :disabled="disabled"
      @change="onChange"
    />
    {{ value }}
  </label>
</template>
<script setup>
import { computed } from "vue";

const props = defineProps({
  id: String,
  value: String,
  disabled: Boolean,
  correctAnswer: String,
});
const model = defineModel();
const emits = defineEmits(["change"]);
const onChange = (event) => {
  emits("change", event);
};
const classes = computed(() => ({
  disabled: props.disabled,
  right: props.disabled && props.value === props.correctAnswer,
  wrong:
    props.disabled &&
    props.value !== props.correctAnswer &&
    model.value === props.value,
}));
</script>
<style>
.disabled {
  opacity: 0.5;
}
.right {
  color: green;
  opacity: 1;
}
.wrong {
  color: red;
  opacity: 1;
}
</style>
