<script setup>
import { defineProps, inject } from 'vue'
const { name } = defineProps(['name'])
const { addToCart } = inject('command')
</script>

<template>
  <button @click="addToCart(name)">Add To Cart</button>
</template>

<style scoped>
button {
  background-color: #6866f0;
  color: white;
  padding: 10px 24px;
  cursor: pointer;
  border: none;
  border-radius: 5px;
}
</style>
