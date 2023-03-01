<!-- // Script is in some way equivalent to script.js. This is place
to define variables, methods and imports of other Vue compoennts. -->
<script setup>
// Import other Vue components in order to add them to a template.
import SliderInput from "./components/SliderInput.vue";
import ToggleInput from "./components/ToggleInput.vue";
import GeometryView from "./components/GeometryView.vue";
import TextInput from "./components/TextInput.vue";
import MyGeometryComponent from "./components/MyGeometryComponent.vue";

// Imports from packages

// Understanding ref article: https://blog.logrocket.com/understanding-vue-refs/#:~:text=Ref%20s%20are%20Vue.,element%20in%20your%20Vue%20instance.
// When ref attribute is added to element, this element then can be referenced
// in template. It is sort of templatecement of getElementById (but better)
import { ref } from "vue";

// Define variables and constants
var count = ref(0);
var firstSlider = ref(25);
var secondSlider = ref(25);
var runToggle = ref(false);


// Define functions
function increment() {
  count.value++;
  //console.log(`Value is: ${count.value}.`);
}

function updateValue(newValue, parameterName) {
  if (parameterName === "Scale_1") {
    firstSlider.value = newValue;
  }
  if (parameterName === "Scale_2") {
    secondSlider.value = newValue;
  }
}

function updateToggle(newValue) {
  runToggle.value = newValue;
  if (newValue === "true") {
    runToggle.value = count;
  }


};




</script>

<!-- Template is a HTML-based syntax that allows you to bind the rendered DOM elements
with data, objects, functions etc. -->
<template>
  <div id="top-bar">
    <div id="title-container">
      <img class="logo-image" alt="Iaac logo" src="./assets/iaac-white.png" />
      <h2>Digital Tools for Cloud-based Data Management</h2>
    </div>
  </div>

  <div id="content">
    <!-- First example -> button -->
    <!-- <button @click="increment">Add one more</button>
    <p>Count is: {{  count }}</p> -->

    <div>
      <!-- Vue component injected into App.vue component template.
      That makes it App.vue a parent and SliderInput.vue a child. -->
      <SliderInput title="Scale_1"
        v-bind:min="1" v-bind:max="50" v-bind:step="1"
        v-on:updateValue="updateValue"/>

      <SliderInput title="Scale_2"
        v-bind:min="1" v-bind:max="50" v-bind:step="1"
        v-on:updateValue="updateValue"/>

      <ToggleInput title="Run to see Geometry_1" v-on:updateValue="updateToggle"></ToggleInput>
      

      <h2>Value received in App.vue: {{ firstSlider }}</h2>
      <h2>Value received in App.vue: {{ secondSlider }}</h2>
      <h2>Value received in App.vue: {{ runToggle }}</h2>
    </div>

    <div v-if="runToggle">
      <GeometryView :size="firstSlider" />
    
  
      <!-- uncomment to add another geometryview -->
      <!-- <GeometryView :size="firstSlider"/> -->
    </div>
    <div id="container">
      <GeometryView :size="secondSlider" />
    
  
      <!-- uncomment to add another geometryview -->
      <!-- <GeometryView :size="firstSlider"/> -->
    </div>

    <div>
    <text-input label="Enter some text" v-model="text" />
    <p>You entered: {{ text }}</p>
  </div>

  </div>
</template>

<!-- Style is for CSS styling -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  height: 100vh;
}

#top-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: rgba(0, 0, 0, 0.7);
}

#title-container {
  display: flex;
  align-items: center;
  color: white;
  margin-right: 1.5rem;
}

#content {
  display: flex;
  justify-content: space-between;
  flex-direction: row; /* Change the default value to row */
}

.item {
  flex-basis: calc(33.33% - 10px);
  height: 100px;
  margin-bottom: 20px;
  width: 48%; /* Adjust the width of the GeometryView component */
}

.inline-block {
  display: flex;
  flex-wrap: nowrap;
  justify-content: space-between;
  flex-direction: row;
}

.logo-image {
  height: 3.25rem;
  padding: 0.5rem;
}

h2 {
  font-size: 1.125rem;
  font-weight: 600;
  letter-spacing: -0.05em;
  font-size: 1.125rem;
  font-weight: 600;
  letter-spacing: 0.01em;
}
</style>
