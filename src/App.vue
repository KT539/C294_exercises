<script setup>
import { ref } from 'vue'
import ProductDisplay from "@/components/ProductDisplay.vue"

const cart = ref(0)

function addToCart() {
    cart.value++
}
function removeFromCart() {
    cart.value--
}
</script>

<template>
  <div id="header">
    <h2>Cart: {{ cart }}</h2>
  </div>
  <div id="app">
    <ProductDisplay />
  </div>
  <div id="cart">
    <button @click="addToCart" class="button">+ Cart</button>
    <button @click="removeFromCart" class="button">- Cart</button>
  </div>
</template>