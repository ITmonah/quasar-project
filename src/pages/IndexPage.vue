<template>
  <div class="row justify-center" style="margin-top: 30px">
    <div class="col-sm-4 col-md-3 col-xs-12">
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
      <q-input
        v-model="search"
        debounce="500"
        filled
        placeholder="Поиск..."
        @change="getStore"
      >
        <template v-slot:append>
          <q-icon name="search" class="search_ic" />
        </template>
      </q-input>
    </div>
  </div>
  <div class="row justify-center product_box">
    <div class="col-md-6 col-xs-11 col-sm-6">
      <div class="row">
        <ProductList :items="arr" />
      </div>
      <div class="q-pa-lg flex flex-center">
        <q-pagination
          v-model="current"
          :max="max_page"
          @click="getStore"
          color="black"
        />
      </div>
    </div>
  </div>
  <div class="footer row justify-center">
    <div class="col-4">
      <div class="row foot_l">
        <div class="col-12 col-md-6 col-sm-6 foot_a">
          <div class="foot_d">
            <a href="#">Главная</a>
            <a href="#">Каталог товаров</a>
            <a href="#">О нас</a>
          </div>
        </div>
        <div class="col-12 col-md-6 col-sm-6 foot_a">
          <div class="foot_k">
            <p>Контакты</p>
            <a href="tel:+7987654321">+7987654321</a>
            <a href="mailto:vasin.sasha26@gmail.com">vasin.sasha26@gmail.com</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import ProductList from "src/components/ProductList.vue";
import { ref } from "vue";

export default defineComponent({
  components: { ProductList },
  name: "IndexPage",
  setup() {
    return {
      current: ref(1),
      search: ref(""),
    };
  },
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
      max_page: 1,
      arr: "",
      fil_cat: 0,
      new_arr: [],
    };
  },
  methods: {
    getStore() {
      let link = document.createElement("a");
      link.setAttribute("href", "#");
      link.click();
      if (this.search != "") {
        this.arr.length = 0;
        this.new_arr.length = 0;
        this.max_page = 0;
        fetch("https://fakestoreapi.com/products")
          .then((res) => res.json())
          .then((json) => {
            this.arr = json;
            for (let index = 0; index < this.arr.length; ++index) {
              if (
                this.arr[index].title
                  .toLowerCase()
                  .includes(this.search.toLowerCase())
              ) {
                this.new_arr.push(this.arr[index]);
              }
            }
            this.arr = this.new_arr;
          });
      } else if (this.cats[this.fil_cat].cat == "all") {
        this.max_page = 2;
        fetch("https://fakestoreapi.com/products")
          .then((res) => res.json())
          .then((json) => {
            this.arr = json;
            if (this.current == 1) {
              this.arr = this.arr.slice(0, 10);
            } else {
              this.arr = this.arr.slice(10, 20);
            }
          });
      } else {
        this.current = 1;
        this.max_page = 1;
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
.search_ic:hover {
  cursor: pointer;
}
.q-field__control,
.q-field__append {
  height: 43px;
}
.q-field__control {
  margin-top: 20px;
}
.foot_k {
  display: flex;
  flex-direction: column;
  gap: 7px;
  align-items: center;
}
.foot_p {
  display: flex;
  justify-content: center;
}
.foot_k p {
  margin: 0;
  margin-top: 14px;
  color: #fff;
  font-size: 18px;
}
.foot_d {
  display: flex;
  flex-direction: column;
  gap: 7px;
}
.foot_a {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.foot_a a {
  text-decoration-line: none;
  color: #fff;
  font-size: 18px;
}
.foot_a p {
  margin: 0;
  color: #fff;
  font-size: 18px;
}
.footer {
  width: 100%;
  min-height: 160px;
  background-color: #000;
  display: flex;
  align-items: center;
}
html {
  scroll-behavior: smooth;
}
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
  min-height: 1000px;
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
@media screen and (max-width: 600px) {
  h1 {
    text-align: center;
  }
}
</style>
