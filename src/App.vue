<script setup>
  import { ref } from 'vue';
  import testImage from './assets/images/socks_blue.jpeg';

  const product = ref('Blue Socks')
  const description = ref('A pair of blue socks with Vue Mastery logo')
  const img = ref(testImage)
  const url = ref('https://www.vuemastery.com/')
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p>{{ description }}</p>
        <a v-bind:href="url">Plus d'informations</a>
        <img v-bind:src="img" />
      </div>
    </div>
  </div>
</template>