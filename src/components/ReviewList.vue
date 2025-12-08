<script setup>
defineProps({
  reviews: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <div v-if="reviews.length">
    <h2>Reviews:</h2>

    <ul>
      <li v-for="(review, index) in reviews" :key="index">
        <p><strong>{{ review.name }}</strong> rated it <strong>{{ review.rating }}</strong>,</p>
        <p>and commented: {{ review.content }}</p>
        <p>
          <strong>Recommend this product:</strong>
          {{ review.recommend }}
        </p>
      </li>
    </ul>
  </div>

  <p v-else>No reviews yet.</p>
</template>