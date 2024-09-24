<script setup lang="ts">
import { computed, ref } from 'vue'

let msg = ref('This is an example of string interpolation')
const htmlElement = `
  <p style="color: red;">
    Hello world! This is color red
  </p>
`

const disabled = ref(true)
setTimeout(() => {
  disabled.value = false
}, 5000)

const styleObject = ref({
  style: 'color: red;'
})
const link = ref('https://konadu.dev')

// Reactivity Fundamentals
function changeMsg() {
  msg.value = 'Changing the message, and seeing if it will work, and it will trigger reactivity'

  author.value.books = []
}

// Computed properties
const author = ref({
  name: 'John Doe',
  books: ['Vue 2 - Advanced Guide', 'Vue 3 - Basic Guide', 'Vue 4 - The Mystery']
})

const publishedBooksMessage = computed(() => (author.value.books.length > 0 ? 'Yes' : 'No'))
// You can access a computed property like so:
publishedBooksMessage.value
</script>

<template>
  <p>Hello there</p>

  <p>Msg: {{ msg }}</p>

  <br />

  <p>String interpolation vs using the v-html directive</p>
  <div>
    <div>
      {{ htmlElement }}
    </div>

    <br />

    <div v-html="htmlElement"></div>
  </div>

  <div>
    <p>Boolean attributes and v-binding</p>
    <button @click="changeMsg" :disabled="disabled">This button is disabled for 5 seconds</button>
  </div>

  <br />

  <div>
    <p>Dynamic attribute names</p>

    <a :href="link" v-bind="styleObject">Click me</a>
  </div>

  <div>
    <p>Computed Properties</p>

    <p>{{ author.name }} is an author. Does he have published books? {{ publishedBooksMessage }}</p>
  </div>
</template>

<style scoped></style>
