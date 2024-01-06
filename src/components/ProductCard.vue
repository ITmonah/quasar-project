<template>
  <div class="col-sm-12 col-lg-4 col-md-6 product_col">
    <q-card class="my-card" flat bordered>
      <div class="card_img">
        <img :src="img" />
      </div>

      <q-card-section>
        <div class="text-h6 q-mb-xs">{{ title }}</div>
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
</template>

<script>
import { defineComponent } from "vue";
import { ref } from "vue";

export default defineComponent({
  name: "ProductCard",
  props: {
    title: String,
    price: Number,
    img: String,
    rate: Number,
    count: Number,
    category: String,
  },
  setup() {
    return {
      stars: ref(0),
    };
  },
});
</script>

<style scoped>
.my-card {
  width: 95%;
}
.card_img {
  width: 100%;
  height: 200px;
  display: flex;
  justify-content: center;
}
.card_img img {
  width: 60%;
  height: 95%;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10px;
  object-fit: contain;
}
</style>