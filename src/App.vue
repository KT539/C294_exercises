<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const details = ref(['50% coton', '30% laine', '20% polyester'])
const variants = ref([{id:2234, color:'green'}, {id:2235, color:'blue'}])
const sizes = ref(['S', 'M', 'L', 'XL'])

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
        <h2>Composition:</h2>
        <ul>
          <li>{{ details[0] }} </li>
          <li>{{ details[1] }}</li>
          <li>{{ details[2] }}</li>
        </ul>
        <h2>Available colors:</h2>
        <ul>
          <li v-for="variant in variants">
            {{ variant.color }}
          </li>
        </ul>
        <h2>Available sizes:</h2>
        <ul>
          <li v-for="size in sizes">
            {{ size }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>