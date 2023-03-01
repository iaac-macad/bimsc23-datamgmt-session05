<!-- // Script is in some way equivalent to script.js. This is place
to define variables, methods and imports of other Vue compoennts. -->
<script setup>
// Import other Vue components in order to add them to a template.

// Imports from packages

// Understanding ref article: https://blog.logrocket.com/understanding-vue-refs/#:~:text=Ref%20s%20are%20Vue.,element%20in%20your%20Vue%20instance.
// When ref attribute is added to element, this element then can be referenced
// in template. It is sort of templatecement of getElementById (but better)
import { ref } from "vue";

// Define variables and constants
var count = ref(0);

//Props
const props = defineProps ([ 'title' ])

var titleFromParent = props.title

console.log(props.title)

//Emits

const emits = defineEmits ([ 'updateCount'])

// Define functions
function increment() {
  count.value++;
  //console.log(`Value is: ${count.value}.`);
  emits('updateCount', count.value) 
}




</script>

<!-- Template is a HTML-based syntax that allows you to bind the rendered DOM elements
with data, objects, functions etc. -->
<template>
  
  <div id="content">
    <button @click="increment">{{ titleFromParent }}</button>
    <P>Count is: {{ count }}</P>
  </div>


</template>