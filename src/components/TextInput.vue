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

// Define emits that you want to send to parent
const emits = defineEmits(["updateTextInputValue"]);

// Define variables that you want to use
var textInputValue = ref("default text");

// Define function that is called v-on:input in your input component (in tempate)
function updateTextInputValue() {
  // emit a function called updateTextInputValue (define in emits) with updated value
  emits("updateTextInputValue", textInputValue.value);
}
</script>
