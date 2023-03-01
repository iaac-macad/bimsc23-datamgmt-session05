<template>
  <div>
    <label>{{ label }}</label>
    <input type="text" v-model="value">
  </div>
</template>

<script>

function updateTextInputValue(newValue) {
  textInputValue.value = newValue;
  appContext.emit('updateTextInputValue', textInputValue.value);
}

</script>
