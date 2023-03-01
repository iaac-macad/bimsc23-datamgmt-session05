<template>
  <div>
    <label>{{ label }}</label>
    <input
      type="text"
      v-model="textInputValue"
      v-on:input="updateTextInputValue"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
// Define properties that should come from a parent
const props = defineProps(["label"]);
const emits = defineEmits(["updateTextInputValue"]);

var textInputValue = ref("default text");

// Define function to emit value form this component to parent
function updateTextInputValue() {
  emits("updateTextInputValue", textInputValue.value);
}
</script>
