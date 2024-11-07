<script setup>
import titleComponent from './components/TitleComponent.vue'
import menuItem from './components/MenuItem.vue'
import { roundTwo } from './helpers/roundTwo.js'
import { watch } from 'vue'
import { ref } from 'vue'
import { provide } from 'vue'

// Variable per guardar la informació del menú, la moneda i els preus
let info = ref({
  currency: 'Dollars',
  menu: [
    { name: 'Hamburger 🍔', price: 5 },
    { name: 'Cheeseburger 🧀', price: 6 },
    { name: 'Impossible Burger 🥕', price: 7 },
    { name: 'Fries 🍟', price: 2 }
  ]
})

// Funció per actualitzar la info, com ara la moneda o els plats
const updateInfo = (key, value) => {
  info.value[key] = value
}
// Funció per actualitzar els preus del menú quan canviem de moneda
const updateMenu = (currency) => {
  if (currency === 'Dollars') {
    info.value.menu.forEach((item) => {
      item.price = roundTwo(item.price * 1.08)
    })
  } else {
    info.value.menu.forEach((item) => {
      item.price = roundTwo(item.price / 1.08)
    })
  }
}
// Watcher per actualitzar la vista quan canviem de moneda
watch(
  () => info.value.currency,
  (currency) => {
    updateMenu(currency)
  }
)
// Variable per guardar la comanda del client
let command = ref({
  title: '',
  cart: []
})
// Funció per afegir un plat al carret de la comanda del client
const addToCart = (item) => {
  command.value.cart.push(item)
  //console.log('Cart:', item)
  //console.log('cart:', command.value.cart)
}
// Funció per finalitzar la comanda
const placeOrder = () => {
  alert('Order placed: ' + command.value.title + '=>' + command.value.cart)
}

provide('info', { info, updateInfo })
provide('command', { command, addToCart, placeOrder })
</script>

<template>
  <div>
    <titleComponent />
    <form>
      <select name="currency" v-model="info.currency">
        <option value="Dollars">Dollars($)</option>
        <option value="Euros">Euros(€)</option>
      </select>
    </form>
    <h3>Menu</h3>
    <menuItem
      v-for="item in info.menu"
      :name="item.name"
      :price="item.price"
      :currency="info.currency"
      v-bind:key="item.name"
    />
  </div>
</template>

<style scoped>
h3 {
  display: flex;
  justify-content: center;
  margin: 0.5em;
  color: #6866f0;
}
form {
  display: flex;
  justify-content: center;
  margin: 0.5em;
}
select {
  padding: 0.5em;
  font-size: 1em;
  border-radius: 0.5em;
  border: 1px solid #6866f0;
}
</style>
