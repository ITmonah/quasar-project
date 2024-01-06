<script>
import { ref } from "vue";

export default {
  name: "ModalWindow",
  props: {
    title: String,
    price: Number,
    img: String,
    rate: Number,
    count: Number,
    category: String,
    description: String,
  },
  methods: {
    close() {
      this.$emit("close");
    },
  },
  setup() {
    return {
      stars: ref(0),
    };
  },
};
</script>

<template>
  <div class="modal-backdrop">
    <div class="modal">
      <button type="button" class="btn-close" @click="close">x</button>
      <div class="col-sm-12 col-lg-4 col-md-6 product_col">
        <q-card class="my-card" flat bordered>
          <div class="card_img">
            <img :src="img" />
          </div>

          <q-card-section>
            <div class="text-h6 q-mb-xs">{{ title }}</div>
            <div class="row no-wrap items-center">
              <q-rating size="18px" v-model="stars" :max="5" color="primary" />
              <span class="text-caption text-grey q-ml-sm"
                >{{ rate }} ({{ count }})</span
              >
            </div>
            <div class="q-mb-xs" style="color: #818181; font-size: 16px">
              Категория: {{ category }}
            </div>
            <div class="q-mb-xs" style="font-size: 16px">
              {{ description }}
            </div>
            <div class="text-h6 q-mb-xs" style="color: #023e8a">
              Цена: {{ price }} $
              <button type="button" class="btn-green" @click="close">
                В корзину
              </button>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </div>
</template>

<style>
.card_img {
  width: 100%;
  height: 400px;
  display: flex;
  justify-content: center;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
}

.modal {
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  border-bottom: 1px solid #eeeeee;
  color: #4aae9b;
  justify-content: space-between;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  justify-content: flex-end;
}

.modal-body {
  position: relative;
  padding: 20px 10px;
}

.btn-close {
  border: none;
  font-size: 20px;
  padding: 20px;
  cursor: pointer;
  font-weight: bold;
  color: #4aae9b;
  background: transparent;
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
}
</style>