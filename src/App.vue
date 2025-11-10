<script setup>
import {computed, ref} from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const inStock = ref(true)
const details = ref(['50% cotton', '30% wool', '20% polyester'])
const variants = ref([{id:2234, color:'green', image: socksGreenImage, quantity:10}, {id:2235, color:'blue', image: socksBlueImage, quantity:0}])
const cart = ref(0)
const brand = ref('CPNV')
const productTitle = computed(() => {
  return `${brand.value} ${product.value}`
})

function addToCart() {
  if (inStock.value) {
    cart.value++
  } else {
    alert('This product is out of stock!')
  }
}
function removeFromCart() {
  if (cart.value > 0) {
    cart.value--
  }
}
function changeImage(variantImage) {
  image.value = variantImage
}
</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img v-bind:src="image" v-bind:class="{ 'out-of-stock-img': !inStock}">
      </div>
      <div class="product-info">
        <h1>{{ productTitle }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <h2>Composition:</h2>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <h2>Available colors:</h2>
        <div
            v-for="variant in variants"
            :key="variant.id"
            class="color-circle"
            :style="{ backgroundColor: variant.color, cursor: 'pointer' }"
            @mouseover="changeImage(variant.image)"
        >
        </div>
        <h2>Available sizes:</h2>
        <ul>
          <li v-for="size in sizes">
            {{ size }}
          </li>
        </ul>
        <button @click="addToCart"
                class="button"
                v-bind:disabled="!inStock"
                v-bind:class="{ 'disabledButton': !inStock }"
        >
          + Cart
        </button>
        <button @click="removeFromCart"
                class="button"
                v-bind:disabled="cart <= 0"
                v-bind:class="{ 'disabledButton': cart <=0 }"
        >
          - Cart
        </button>
      </div>
    </div>
  </div>
</template>