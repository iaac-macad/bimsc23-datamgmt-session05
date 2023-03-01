<script setup>
import { ref } from "vue";
// Define properties that you will be able to access from parent component. 
// Those properties will be binded from parent to child. 
// Available JavaScript types: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures
const props = defineProps(['title', 'min', 'max', 'step'])

const titlec = ref(props.title)
// Define events that will be accessible from parent component
const emits = defineEmits(['updateValue'])



var sliderValue = ref(20)

function sendValueUpate()
{
  emits('updateValue', sliderValue.value, titlec.value)
}


</script>

<template>
<div>
	<form class="definition-input">
			<label class="input-title" for="range-slider">{{ title }}: {{ sliderValue }}</label>

			<input type="range" class="modern-range"
			v-bind:min="min" v-bind:max="max" v-bind:step="step"
			v-model="sliderValue" 
      v-on:input="sendValueUpate"
			/>
	</form>
</div>


</template>

<style scoped>
.modern-range {
  -webkit-appearance: none;
  width: 100%;
  background: linear-gradient(90deg, #f19af3, #f099b5);
  height: 17px;
  border-radius: 15px;
  margin: 10px 0px;
}

.modern-range::-webkit-slider-thumb {
  -webkit-appearance: none;
  height: 15px;
  width: 15px;
  border-radius: 15px;
  background-color: black;
  cursor: pointer;
}
</style>