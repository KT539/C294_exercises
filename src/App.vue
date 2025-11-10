<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const inStock = true
const details = ref(['50% cotton', '30% wool', '20% polyester'])
const variants = ref([{id:2234, color:'green', image: socksGreenImage}, {id:2235, color:'blue', image: socksBlueImage}])
const sizes = ref(['S', 'M', 'L', 'XL'])
const cart = ref(0)

function addToCart() {
  cart.value++
}
function removeFromCart() {
  cart.value--
}
function changeImage(variantImage) {
  image.value = variantImage
}
</script>
  
<template>
  <div class="nav-bar">
    <p>Cart : {{ cart }}</p>
  </div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img v-bind:src="image" alt="product image">
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <h2>Composition:</h2>
        <ul>
          <li v-for="detail in details">
            {{ detail }}
          </li>
        </ul>
        <h2>Available colors:</h2>
        <ul>
          <li v-for="variant in variants"
          @mouseover="changeImage(variant.image)">
            {{ variant.color }}
          </li>
        </ul>
        <h2>Available sizes:</h2>
        <ul>
          <li v-for="size in sizes">
            {{ size }}
          </li>
        </ul>
        <button @click="addToCart">Add To Cart</button>
        <button @click="removeFromCart">Remove From Cart</button>
      </div>
    </div>
  </div>
</template>