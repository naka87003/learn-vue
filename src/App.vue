<script setup lang="ts">
import { ref } from 'vue';
import ProductDisplay from '@/components/ProductDisplay.vue';

const cart = ref<number[]>([]);
const premium = ref(false);
const updateCart = (id: number) => {
  cart.value.push(id);
};
const remove = (id: number) => {
  const removeIndex = cart.value.findIndex((value) => value === id);
  console.log(removeIndex);
  if (removeIndex != undefined) {
    cart.value = cart.value.filter((value, index) => {
      return index !== removeIndex;
    });
  }
};
</script>

<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart.length }})</div>
  <ProductDisplay :premium @addToCart="updateCart" @remove="remove" />
</template>
