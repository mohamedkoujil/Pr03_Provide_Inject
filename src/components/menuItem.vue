<script setup>
import addCartBtn from './addCartBtn.vue'
import { defineProps, computed } from 'vue'
const { name, price, currency } = defineProps(['name', 'price', 'currency'])

const currencySymbol = computed(() => {
  return currency === 'Dollars' ? '$' : '€'
})
</script>

<template>
  <div class="container">
    <div class="flex-column margin-right">
      <span>{{ name }} </span>
      <span>{{ price }}{{ currencySymbol }}</span>
    </div>
    <addCartBtn :name="name" />
  </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  border: 1px solid rgb(202, 202, 202);
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
}
.flex-column {
  display: flex;
  flex-direction: column;
}

.margin-right {
  margin-right: 20px;
}
</style>
