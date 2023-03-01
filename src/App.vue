<!-- // Script is in some way equivalent to script.js. This is place
to define variables, methods and imports of other Vue compoennts. -->
<script setup>
// Import other Vue components in order to add them to a template.
import SliderInput from "./components/SliderInput.vue";
import ToggleInput from "./components/ToggleInput.vue";
import GeometryView from "./components/GeometryView.vue";

// Imports from packages

// Understanding ref article: https://blog.logrocket.com/understanding-vue-refs/#:~:text=Ref%20s%20are%20Vue.,element%20in%20your%20Vue%20instance.
// When ref attribute is added to element, this element then can be referenced
// in template. It is sort of templatecement of getElementById (but better)
import { ref } from "vue";
import { conditionalExpression } from "@babel/types";

// Define variables and constants
var slider1 = ref(5);
var slider2 = ref(5);
var slider3 = ref(5);
var slider4 = ref(32);
var runtoggle = ref(true);

// Define functions
function increment() {
  count.value++;
  //console.log(`Value is: ${count.value}.`);
}

function updateValue(newValue, parameterName) {
  if (parameterName === "RadiusTop") {
    slider1.value = newValue;
  }
  if (parameterName === "RadiusBottom") {
    slider2.value = newValue;
  }
  if (parameterName === "Height") {
    slider3.value = newValue;
  }
  if (parameterName === "RadialSegments") {
    slider4.value = newValue;
  }

}
  function updateToggle(newValue) {
      runToggle.value = newValue;
}
</script>

<!-- Template is a HTML-based syntax that allows you to bind the rendered DOM elements
with data, objects, functions etc. -->
<template>
  <div id="top-bar">
    <div id="title-container">
      <img class="logo-image" alt="Iaac logo" src="./assets/iaac-white.png" />
      <h2>Digital Tools for Cloud-based Data Management l Sara Kessba Assigment 03</h2>
    </div>
  </div>

  <div id="content">
    <!-- First example -> button -->
    <!-- <button @click="increment">Add one more</button>
    <p>Count is: {{  count }}</p> -->

    <div>
      <!-- Vue component injected into App.vue component template.
      That makes it App.vue a parent and SliderInput.vue a child. -->
      <SliderInput title="RadiusTop"
      v-bind:min="0" v-bind:max="10" v-bind:step="1"
      v-on:updateValue="updateValue"/>

      <SliderInput title="RadiusBottom"
      v-bind:min="0" v-bind:max="10" v-bind:step="1"
      v-on:updateValue="updateValue"/>

      <SliderInput title="Height"
      v-bind:min="1" v-bind:max="30" v-bind:step="1"
      v-on:updateValue="updateValue"/>

      <SliderInput title="RadialSegments"
      v-bind:min="1" v-bind:max="32" v-bind:step="1"
      v-on:updateValue="updateValue"/>

      <ToggleInput title="OpenEnded" v-on:updateValue="updateToggle"></ToggleInput>

    </div>

    <div id="content">
      <GeometryView :radiusTop="slider1" :radiusBottom="slider2" :height="slider3" :radialSegments="slider4" :openEnded="runtoggle"/>

      <!-- uncomment to add another geometryview -->
      <!-- <GeometryView :size="firstSlider"/> -->
    </div>
  </div>
</template>

<!-- Style is for CSS styling -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#top-bar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      /*background-color: rgb(0, 0, 0);*/
    }

    #title-container {
      display: flex;
      align-items: center;
      color: white;
      margin-right: 1.5rem;
    }

    #content {
      display: flex;
    }

    .logo-image {
      height: 3.25rem;
      padding: 0.5rem;
    }
    body {
      background: rgb(102, 102, 102);
    }
    h2 {
      font-size: 1.125rem;
      font-weight: 400;
      letter-spacing: -0.05em;
      font-size: 1.125rem;
      font-weight: 400;
      letter-spacing: 0.01em;
      color: white;
    }
</style>
