<!-- // Script is in some way equivalent to script.js. This is place
to define variables, methods and imports of other Vue compoennts. -->
<script setup>
// Import other Vue components in order to add them to a template.
import SliderInput from './components/SliderInput.vue'
import GeometryView from './components/GeometryView.vue'

// Imports from packages

// Understanding ref article: https://blog.logrocket.com/understanding-vue-refs/#:~:text=Ref%20s%20are%20Vue.,element%20in%20your%20Vue%20instance.
// When ref attribute is added to element, this element then can be referenced
// in template. It is sort of templatecement of getElementById (but better)
import { ref } from "vue";
import { store } from './store.js'

// Define variables and constants
var firstSlider = ref(10)


function updateValue(newValue) {
  firstSlider.value = newValue
  store.count= newValue
  console.log(store.count)
}

</script>



<!-- Template is a HTML-based syntax that allows you to bind the rendered DOM elements
with data, objects, functions etc. -->
<template>
  <div id="top-bar">
    <div id="title-container">
      <img class="logo-image" alt="Iaac logo" src="./assets/iaac-white.png" />
      <h2>
        Digital Tools for Cloud-based Data Management
      </h2>
    </div>
  </div>

  <div id="content">

    <!-- This is where another Vue component is injected into template. -->
    <SliderInput 
    title="Height" v-bind:min="0" v-bind:max="100" v-bind:step="10"
    @updateValue="updateValue"/>

    <h2> Value received in App.vue: {{  firstSlider }}</h2>

  </div>
  

 <div class="geometry">

  <GeometryView :val="firstSlider" />

 </div>
</template>

<!-- Style is for CSS styling -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
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
