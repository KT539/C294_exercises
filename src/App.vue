<script setup>
import { ref } from 'vue';
import testImage from './assets/images/socks_blue.jpeg';

const product = ref('Blue Socks')
const description = ref('A pair of blue socks with Vue Mastery logo')
const img = ref(testImage)
const inventory = ref(9)
const inSale = ref(false)
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p>{{ description }}</p>
        <p v-show="inventory>10">In stock</p>
        <p v-show="inventory<10 && inventory>0">Low stock</p>
        <p v-show="!inventory">Out of stock</p>
        <p v-show="inSale">In sale</p>
        <img v-bind:src="img" />
      </div>
    </div>
  </div>
</template>