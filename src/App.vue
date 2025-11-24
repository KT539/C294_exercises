<script setup>
import {computed, ref} from 'vue'
import ProductDisplay from "@/components/ProductDisplay.vue"

const cart = ref({})
const premium = ref(true)

function addToCart(id) {
  if (!cart.value[id]) {
    cart.value[id] = 0;
  }
  cart.value[id]++;
}
function removeFromCart(id) {
    if (cart.value[id] && cart.value[id] > 0) {
      cart.value[id]--
      if (cart.value[id] === 0) {
        delete cart.value[id];
      }
    }
}
const cartTotal = computed(() => {
  return Object.values(cart.value).reduce((sum, qty) => sum + qty, 0);
})
</script>

<template>
  <div id="header">
    <h2>Cart: {{ cartTotal }}</h2>
    <p>User premium: {{ premium }}</p>
  </div>
  <ProductDisplay v-bind:premium="premium" v-bind:cart="cart" @add="addToCart" @remove="removeFromCart" />
  <ProductDisplay v-bind:premium="premium" v-bind:cart="cart" @add="addToCart" @remove="removeFromCart" />
  <ProductDisplay v-bind:premium="premium" v-bind:cart="cart" @add="addToCart" @remove="removeFromCart" />
</template>