<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits<{
  'review-submitted': [review: ProductReview];
}>();

const review = ref<ProductReview>({
  name: '',
  content: '',
  rating: null,
});

const onSubmit = () => {
  if (review.value.name === '' || review.value.content === '' || review.value.rating === null) {
    alert('Review is incomplete. Please fill out every field.');
    return;
  }
  emit('review-submitted', { ...review.value });
  review.value.name = '';
  review.value.content = '';
  review.value.rating = null;
};
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input id="name" v-model="review.name" />

    <label for="review">Review:</label>
    <textarea id="review" v-model="review.content"></textarea>

    <label for="rating">Rating:</label>
    <select id="rating" v-model.number="review.rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>
    <input class="button" type="submit" value="Submit" />
  </form>
</template>
