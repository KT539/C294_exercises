<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image" :class="{ 'out-of-stock-img': !inStock }" />
      </div>
      <div class="product-info">
        <h1>{{ productTitle }}</h1>
        <p>{{ sale }}</p>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>

        <h2>Composition:</h2>
        <ul>
          <li v-for="detail in details" :key="detail">{{ detail }}</li>
        </ul>

        <h2>Available colors:</h2>
        <div
            v-for="(variant, index) in variants"
            :key="variant.id"
            class="color-circle"
            :style="{ backgroundColor: variant.color, cursor: 'pointer' }"
            @mouseover="updateVariant(index)"
        ></div>

        <h2>Available sizes:</h2>
        <ul>
          <li v-for="size in sizes" :key="size">{{ size }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import socksGreenImage from "@/assets/images/socks_green.jpeg";
import socksBlueImage from "@/assets/images/socks_blue.jpeg";

export default {
  name: "ProductDisplay",

  data() {
    return {
      product: "Socks",
      brand: "CPNV",
      onSale: true,
      details: ["50% cotton", "30% wool", "20% polyester"],
      sizes: ["S", "M", "L", "XL"],
      selectedVariant: 0,
      variants: [
        { id: 2234, color: "green", image: socksGreenImage, quantity: 10 },
        { id: 2235, color: "blue", image: socksBlueImage, quantity: 0 }
      ]
    };
  },

  methods: {
    updateVariant(index) {
      this.selectedVariant = index;
    }
  },

  computed: {
    productTitle() {
      return `${this.brand} ${this.product}`;
    },
    image() {
      return this.variants[this.selectedVariant].image;
    },
    inStock() {
      return this.variants[this.selectedVariant].quantity > 0;
    },
    sale() {
      return this.onSale ? "This product is on sale." : "";
    }
  }
};
</script>