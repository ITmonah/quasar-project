<template>
  <q-input v-model="search" debounce="500" filled placeholder="Поиск...">
    <template v-slot:append>
      <q-icon name="search" />
    </template>
  </q-input>
</template>

<script>
import { defineComponent } from "vue";
import { ref } from "vue";

export default defineComponent({
  name: "SearchInput",
  setup() {
    return {
      stars: ref(""),
    };
  },
});
</script>
<style>
.q-field__control,
.q-field__append {
  height: 43px;
}
.q-field__control {
  margin-top: 20px;
}
</style>