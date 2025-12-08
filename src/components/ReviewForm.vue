<script setup>
import { reactive } from 'vue'

// emits
const emit = defineEmits(['review-submitted'])

// data
const review = reactive({
  name: '',
  content: '',
  rating: null,
  recommend: ''
})

// methods
function onSubmit() {
  // data validation
  if (
      review.name === '' ||
      review.content === '' ||
      review.rating === null ||
      review.recommend === ''
  ) {
    alert("A field is empty. Please fill in your name, your review and a rating.")
    return
  }

  // create the object
  const productReview = {
    name: review.name,
    content: review.content,
    rating: review.rating,
    recommend: review.recommend,
  }

  // emit to the parent
  emit('review-submitted', productReview)

  // reset the fields
  review.name = ''
  review.content = ''
  review.rating = null
  review.recommend = ''
}
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>

    <label for="name">Name:</label>
    <input id="name" v-model="review.name">

    <label for="review">Review:</label>
    <textarea id="review" v-model="review.content"></textarea>

    <label for="rating">Rating:</label>
    <select id="rating" v-model.number="review.rating">
      <option disabled value="">Select a rating</option>
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <label for="recommend">Would you recommend this product ?</label>
    <select id="recommend" v-model="review.recommend">
      <option disabled value="">Select an option</option>
      <option>Yes</option>
      <option>No</option>
    </select>

    <input class="button" type="submit" value="Submit">
  </form>
</template>