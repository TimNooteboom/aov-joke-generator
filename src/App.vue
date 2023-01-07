<template>
  <div style="margin-top: 30%; margin-left:25%">
    <div class="text-3xl">{{joke}}</div>
    <div v-if="showAnswer">{{ans}}</div>
    <div>
      <button v-if="!showAnswer" @click="jokeAnswer">Show Answer</button>
      <button style="margin-top:25px" @click="getJoke">New Joke</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
let joke = ref(null)
let ans = ref(null)
let showAnswer = ref(false)

const getJoke = async() => {
  showAnswer.value = false
  try {
    const res = await fetch('https://v2.jokeapi.dev/joke/christmas').then(response => response.json())
    joke.value = res.setup
    ans.value = res.delivery
  } catch (error) {
      console.error(error)
      alert('Something went wrong! The joke could not load.')
  }
}

const jokeAnswer = () => {
  showAnswer.value = true
}
getJoke()

</script>

<style>
  button {
    width: 130px;
    border: 1px solid;
    display: block;
  }
</style>
