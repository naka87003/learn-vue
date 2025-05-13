<script setup lang="ts">
import { ref, computed } from 'vue';
import socksGreenImage from '@/assets/images/socks_green.jpeg';
import socksBlueImage from '@/assets/images/socks_blue.jpeg';
import ProductDetails from './ProductDetails.vue';
import ReviewForm from './ReviewForm.vue';
import ReviewList from './ReviewList.vue';

const props = defineProps<{
  premium: boolean;
}>();

const emit = defineEmits<{
  addToCart: [id: number];
  remove: [id: number];
}>();

const product = ref('Socks');
const brand = ref('Vue Mastery');

const selectedVariant = ref(0);

const details = ref(['50% cotton', '30% wool', '20% polyester']);

const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage, quantity: 50 },
  { id: 2235, color: 'blue', image: socksBlueImage, quantity: 0 },
]);

const reviews = ref<ProductReview[]>([]);

const title = computed(() => {
  return brand.value + ' ' + product.value;
});

const image = computed(() => {
  return variants.value[selectedVariant.value].image;
});

const inStock = computed(() => {
  return variants.value[selectedVariant.value].quantity > 0;
});

const shipping = computed(() => {
  if (props.premium) {
    return 'Free';
  } else {
    return 2.99;
  }
});

const addToCart = () => {
  emit('addToCart', variants.value[selectedVariant.value].id);
};

const remove = () => {
  emit('remove', variants.value[selectedVariant.value].id);
};

const updateVariant = (index: number) => {
  selectedVariant.value = index;
};

const addReview = (review: ProductReview) => {
  reviews.value.push(review);
};
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img v-bind:src="image" />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <p>Shipping: {{ shipping }}</p>
        <ProductDetails :details />
        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          @mouseover="updateVariant(index)"
          class="color-circle"
          :style="{ backgroundColor: variant.color }"
        ></div>
        <button
          class="button"
          :class="{ disabledButton: !inStock }"
          :disabled="!inStock"
          @click="addToCart"
        >
          Add to cart
        </button>
        <button class="button" @click="remove">Remove</button>
      </div>
    </div>
    <ReviewList v-if="reviews.length > 0" :reviews />
    <ReviewForm @review-submitted="addReview" />
  </div>
</template>
