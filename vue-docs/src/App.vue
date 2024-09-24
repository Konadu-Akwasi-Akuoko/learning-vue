<script setup lang="ts">
const msg = "This is an example of string interpolation"
const htmlElement = `
  <p style="color: red;">
    Hello world! This is color red
  </p>
`
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
</template>

<style scoped></style>
