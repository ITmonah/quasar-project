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
      <div class="btn_close_box">
        <button type="button" class="btn-close" @click="close">x</button>
      </div>
      <div class="col-sm-6 col-lg-4 col-md-6 product_col">
        <q-card class="my-card" flat bordered style="border: none">
          <div class="card_img">
            <img :src="img" />
          </div>

          <q-card-section>
            <div class="text-h6 q-mb-xs desc_m">{{ title }}</div>
            <div class="row no-wrap items-center">
              <q-rating size="18px" v-model="stars" :max="5" color="primary" />
              <span class="text-caption text-grey q-ml-sm"
                >{{ rate }} ({{ count }})</span
              >
            </div>
            <div class="q-mb-xs cat_m" style="color: #818181; font-size: 16px">
              Категория: {{ category }}
            </div>
            <div class="q-mb-xs desc_m" style="font-size: 16px">
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
.card_img img {
  width: 60%;
  height: 95%;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10px;
  object-fit: contain;
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
.btn_close_box {
  width: 100%;
  height: 40px;
  display: flex;
  justify-content: end;
  align-items: center;
}
.modal {
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
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
.cat_m {
  margin-bottom: 6px;
  margin-top: 6px;
}
.modal-body {
  position: relative;
  padding: 20px 10px;
}

.btn-close {
  border: none;
  font-size: 30px;
  padding-right: 15px;
  cursor: pointer;
  font-weight: bold;
  color: #3a7de0;
  background: transparent;
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
  cursor: pointer;
}
.btn-green:hover {
  background: #59d1bb;
  transition: all 0.1s ease;
}
.desc_m {
  width: 600px;
}
@media screen and (max-width: 900px) {
  .modal {
    width: 80%;
    height: 80%;
  }
}
</style>