<template>
  <ProductCard
    @click="showModal"
    v-for="item in items"
    :key="item.id"
    :title="item.title"
    :price="item.price"
    :img="item.image"
    :rate="item.rating.rate"
    :count="item.rating.count"
    :category="item.category"
  />
  <ModalWindow v-show="isModalVisible" @close="closeModal" />
</template>

<script setup>
import ProductCard from "./ProductCard.vue";
import ModalWindow from "./ModalWindow.vue";

defineProps({
  items: Array,
});
</script>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      isModalVisible: false,
    };
  },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
  },
});
</script>
