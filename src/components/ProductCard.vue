<template>
  <div class="col-xs-12 col-md-6 product_col">
    <q-card class="my-card" flat bordered>
      <div class="card_img" @click="showModal">
        <img :src="img" />
      </div>

      <q-card-section>
        <div class="text-h6 q-mb-xs title_h" @click="showModal">
          {{ title }}
        </div>
        <div class="q-mb-xs" style="color: #818181; font-size: 16px">
          Категория: {{ category }}
        </div>
        <div class="text-h6 q-mb-xs" style="color: #023e8a">{{ price }} $</div>
        <div class="row no-wrap items-center">
          <q-rating size="18px" v-model="stars" :max="5" color="primary" />
          <span class="text-caption text-grey q-ml-sm"
            >{{ rate }} ({{ count }})</span
          >
        </div>
      </q-card-section>
    </q-card>
  </div>
  <ModalWindow
    v-show="isModalVisible"
    @close="closeModal"
    :title="title"
    :category="category"
    :price="price"
    :rate="rate"
    :count="count"
    :img="img"
    :description="description"
  />
</template>

<script>
import { defineComponent } from "vue";
import { ref } from "vue";
import ModalWindow from "./ModalWindow.vue";

export default defineComponent({
  name: "ProductCard",
  components: { ModalWindow },
  props: {
    title: String,
    price: Number,
    img: String,
    rate: Number,
    count: Number,
    category: String,
    description: String,
  },
  data() {
    return {
      isModalVisible: false,
    };
  },
  setup() {
    return {
      stars: ref(0),
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

<style scoped>
.my-card {
  width: 95%;
}
.card_img {
  width: 100%;
  height: 300px;
  display: flex;
  justify-content: center;
  opacity: 0;
  animation: ani 0.5s forwards;
}
@keyframes ani {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
.card_img img:hover {
  width: 64%;
  height: 99%;
  cursor: pointer;
  transition: all 0.1s ease;
}
.card_img img {
  width: 60%;
  height: 95%;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10px;
  object-fit: contain;
}
.title_h:hover {
  color: #3a7de0;
  cursor: pointer;
  transition: all 0.1s ease;
}
</style>