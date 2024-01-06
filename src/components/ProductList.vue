<template>
  <ProductCard
    v-for="item in items"
    :key="item.id"
    :title="item.title"
    :price="item.price"
    :img="item.image"
    :rate="item.rating.rate"
    :count="item.rating.count"
    :category="item.category"
    :description="item.description"
  />
</template>

<script setup>
import ProductCard from "./ProductCard.vue";

defineProps({
  items: Array,
});
</script>
