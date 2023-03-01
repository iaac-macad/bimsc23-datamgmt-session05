<script setup>
import { ref } from "vue"
import html2canvas from "html2canvas"

// Define props
defineProps(['title'])

// Define emits
const emits = defineEmits(['updateValue'])

// Define variables with refs
var toggleValue = ref(false)

// Define functions
function sendToggleUpdate() {
    emits('updateValue', toggleValue.value)
    
        
    
    //console.log(`from child component ${toggleValue.value}`)
}
</script>


<template>
    <form class = "definition-input">
        <label class="input-title" for="toggle"> {{ title }}</label>

        <div class="checkbox-wrapper-22">
        <label class="switch" for="checkbox">
            <input type="checkbox" id="checkbox" 
            v-model="toggleValue" 
            v-on:change="sendToggleUpdate"/>

            <div class="slider round"></div>
        </label>
        </div>
    </form>
</template>