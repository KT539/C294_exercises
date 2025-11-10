<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const inStock = true
const details = ref(['50% cotton', '30% wool', '20% polyester'])
const cart = ref(0)
</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img v-bind:src="image">
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
      </div>
    </div>
  </div>
</template>