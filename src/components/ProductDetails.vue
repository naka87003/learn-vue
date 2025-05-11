<script setup lang="ts">
defineProps<{
  details: string[];
}>();
</script>
<template>
  <ul>
    <li v-for="detail in details">{{ detail }}</li>
  </ul>
</template>
