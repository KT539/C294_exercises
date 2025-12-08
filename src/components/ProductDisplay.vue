
<script setup>
import { ref, computed } from 'vue';
import socksGreenImage from "@/assets/images/socks_green.jpeg";
import socksBlueImage from "@/assets/images/socks_blue.jpeg";
import ReviewForm from "@/components/ReviewForm.vue";
import ReviewList from "@/components/ReviewList.vue";


// props & emits
const emit = defineEmits(["add", "remove"]);

const props = defineProps ({
  premium: {
    type: Boolean,
    required: true,
  },
  cart: {
    type: Object,
    required: true,
  }
});

// data
const reviews = ref([])
const product = ref("Socks");
const brand = ref("CPNV");
const onSale = ref(true);
const details = ref(["50% cotton", "30% wool", "20% polyester"]);
const sizes = ref(["S", "M", "L", "XL"]);
const selectedVariant = ref(0);
const variants = ref([
  { id: 2234, color: "green", image: socksGreenImage, quantity: 10 },
  { id: 2235, color: "blue", image: socksBlueImage, quantity: 5 },
]);

// methods
function updateVariant(index) {
  selectedVariant.value = index;
}

function add() {
  emit("add", variants.value[selectedVariant.value].id);
}

function remove() {
  emit("remove", variants.value[selectedVariant.value].id);
}

function addReview(review) {
  reviews.value.push(review)
}

// computed
const productTitle = computed(() => `${brand.value} ${product.value}`);
const image = computed(() => variants.value[selectedVariant.value].image);
const inStock = computed(() => variants.value[selectedVariant.value].quantity > 0);
const sale = computed(() => (onSale.value ? "This product is on sale." : ""));
const shipping = computed(() =>
    props.premium ? "Free shipping" : "Shipping: 5.99 CHF"
)
const cartQuantity = computed(() => {
  const id = variants.value[selectedVariant.value].id
  return props.cart[id] || 0
})

</script>


<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image" :class="{ 'out-of-stock-img': !inStock }" />
      </div>
      <div id="cart">
        <button @click="add"
                class="button"
                v-bind:disabled="!inStock"
                v-bind:class="{ 'disabledButton': !inStock }">
          + Cart
        </button>
        <button @click="remove"
                class="button"
                v-bind:disabled="!inStock || cartQuantity === 0"
                v-bind:class="{ 'disabledButton': !inStock || cartQuantity === 0 }">
          - Cart
        </button>
      </div>
      <div class="product-info">
        <h1>{{ productTitle }}</h1>
        <p>{{ sale }}</p>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <p>{{ shipping }}</p>

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
  <ReviewForm @review-submitted="addReview" />
  <ReviewList :reviews="reviews" />
</template>