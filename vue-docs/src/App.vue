<script setup lang="ts">
import { computed, onMounted, onUpdated, ref } from 'vue'

onMounted(() => {
  console.log('The component is mounted')
})

onUpdated(() => {
  console.log('Update happened')
})

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

// Writable computed, IT IS A BAD PRACTICE, DON'T DO THIS INSIDE YOUR CODE, RATHER MUTATE
// THE DERIVED REF(author.value.name) SO THAT THE COMPUTED VALUE WILL BE COMPUTED AGAIN,
// AS IT IS A DERIVED REF
const splitAuthorName = computed({
  get() {
    return {
      firstName: author.value.name.split(' ')[0],
      secondName: author.value.name.split(' ').slice(1).join(' ')
    }
  },
  set(value: string) {
    author.value.name = value
  }
})

function changeAuthorName() {
  splitAuthorName.value = 'Kwadwo Nkansah Liwin Ani Potwe Potwe'
}

// Class and style bindings
const isActive = ref(false)
</script>

<template>
  <div>
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

      <p>
        {{ author.name }} is an author. Does he have published books? {{ publishedBooksMessage }}
      </p>

      <p>Writable Computed</p>
      <p>
        Split author name = {{ splitAuthorName.firstName }} and {{ splitAuthorName.secondName }}
      </p>

      <button @click="changeAuthorName">Change Author Name</button>
    </div>

    <div>
      <p
        :class="{ active: isActive }"
        @click="
          () => {
            isActive = !isActive
          }
        "
      >
        Class and style bindings. Click on this to change the color
      </p>
    </div>
  </div>
</template>

<style scoped>
.active {
  color: blue;
}
</style>
