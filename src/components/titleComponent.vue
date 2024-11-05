<script setup>
import { inject } from 'vue'
import { computed } from 'vue'

const { command, placeOrder } = inject('command')

const title = computed(() => command.value.title || 'No title')
</script>

<template>
  <h1>{{ title }}</h1>
  <form @submit.prevent="placeOrder">
    <input type="text" name="title" v-model="command.title" placeholder="Titol de la comanda" />
    <button type="submit">Place Order</button>
  </form>
</template>

<style scoped>
h1 {
  display: flex;
  justify-content: center;
  color: #6866f0;
  margin: auto;
}
form {
  width: 100%;
  display: flex;
  flex-direction: column;
}
input {
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 6px;
}

button {
  width: 100%;
  padding: 10px;
  border: none;
  border-radius: 6px;
  background-color: #6866f0;
  color: white;
  font-size: 16px;
  cursor: pointer;
}
</style>
