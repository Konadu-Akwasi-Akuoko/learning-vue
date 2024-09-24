<script setup lang="ts">
import { ref } from 'vue';

const msg = "This is an example of string interpolation"
const htmlElement = `
  <p style="color: red;">
    Hello world! This is color red
  </p>
`

const disabled = ref(true)
setTimeout(() => {
  disabled.value = false;
}, 5000)

const styleObject = ref({
  style: "color: red;"
});
const link = ref('https://konadu.dev')

</script>

<template>
  <p>
    Hello there
  </p>


  <p> Msg: {{ msg }} </p>

  <br />

  <p> String interpolation vs using the v-html directive</p>
  <div>
    <div>
      {{ htmlElement }}
    </div>

    <br />

    <div v-html="htmlElement"></div>
  </div>

  <div>
    <p>Boolean attributes and v-binding</p>
    <button :disabled="disabled">This button is disabled for 5 seconds</button>
  </div>

  <br />

  <div>
    <p>Dynamic attribute names</p>

    <a :href="link" v-bind="styleObject">Click me</a>
  </div>
</template>

<style scoped></style>
