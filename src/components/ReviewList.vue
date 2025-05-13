<script setup lang="ts">
defineProps<{
  reviews: ProductReview[];
}>();
</script>

<template>
  <div class="review-container">
    <h3>Review:</h3>
    <ul>
      <li v-for="(review, index) in reviews" :key="index">
        <span>{{ review.name }} gave this {{ review.rating }} stars</span>
        <br />
        <span>{{ review.content }}</span>
      </li>
    </ul>
  </div>
</template>
