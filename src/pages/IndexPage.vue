<template>
  <div class="row justify-center" style="margin-top: 30px">
    <div class="col-4 col-md-3">
      <h1>Каталог товаров</h1>
    </div>
    <div class="col-auto col-md-1">
      <div class="filt">
        <h2>Категории</h2>
        <select class="sel_f" v-model="fil_cat" @change="getStore">
          <option value="0">Все</option>
          <option value="1">men's clothing</option>
          <option value="2">jewelery</option>
          <option value="3">electronics</option>
          <option value="4">women's clothing</option>
        </select>
      </div>
    </div>
    <div class="col-auto col-md-2">
      <SearchInput />
    </div>
  </div>
  <div class="row justify-center product_box">
    <div class="col-6">
      <div class="row">
        <ProductList :items="arr" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const sortBy = ref("");

const onChangeSelect = (event) => {
  sortBy.value = event.target.value;
};
</script>

<script>
import { defineComponent } from "vue";
import ProductList from "src/components/ProductList.vue";
import SearchInput from "src/components/SearchInput.vue";

export default defineComponent({
  components: { ProductList, SearchInput },
  name: "IndexPage",
  data() {
    return {
      cats: [
        {
          cat: "all",
        },
        {
          cat: "men's clothing",
        },
        {
          cat: "jewelery",
        },
        {
          cat: "electronics",
        },
        {
          cat: "women's clothing",
        },
      ],
      arr: "",
      fil_cat: 0,
    };
  },
  methods: {
    getStore() {
      if (this.cats[this.fil_cat].cat == "all") {
        fetch("https://fakestoreapi.com/products")
          .then((res) => res.json())
          .then((json) => {
            this.arr = json;
          });
      } else {
        fetch(
          "https://fakestoreapi.com/products/category/" +
            this.cats[this.fil_cat].cat
        )
          .then((res) => res.json())
          .then((json) => {
            this.arr = json;
          });
      }
    },
  },
  mounted() {
    this.getStore();
  },
});
</script>

<style>
h1 {
  margin: 0;
  color: #000;
  font-size: 36px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
  margin-top: 20px;
}
.product_col {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}
.product_box {
  margin-top: 40px;
}
.filt {
  padding: 0;
  margin-right: 10px;
}
.sel_f {
  width: 100%;
  padding: 0;
  height: 43px;
  border: 0;
  background: #000;
  border-radius: 4px;
  color: #fff;
}
h2 {
  margin: 0;
  margin-bottom: 3px;
  color: #7e7e7e;
  font-size: 14px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
}
</style>
