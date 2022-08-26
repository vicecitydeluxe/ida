<template>
  <div class="header">
    <Header />
    <Dropdown
      @change="sortByCategory"
      :modelValue="selectedOption"
      :options="sortOptions"
      v-model="selectedOption"
    />
  </div>

  <div class="layout_container">
    <Search @create="createItem" />

    <div class="item_container">
      <transition-group name="item-list">
        <Item
          v-for="item in items"
          :key="item"
          :item="item"
          @remove="removeItem"
        />
      </transition-group>
    </div>
  </div>
</template>

<script setup>
import Search from "./components/Search.vue";
import Header from "./components/Header.vue";
import Item from "./components/Item.vue";
import Dropdown from "./components/Dropdown.vue";
import { ref, onMounted, watch } from "@vue/runtime-core";

const items = ref([]);
const selectedOption = ref("По умолчанию");

const sortOptions = ref([
  { name: "По умолчанию", value: "default" },
  { name: "По цене max", value: "priceMax" },
  { name: "По цене min", value: "priceMin" },
  { name: "По названию", value: "title" },
]);

const createItem = (item) => {
  items.value.push(item);
};
const removeItem = (item) => {
  items.value = items.value.filter((p) => p !== item);
};

const sortByCategory = () => {
  if (selectedOption.value === "По названию") {
    items.value.sort((a, b) => (a["itemName"] > b["itemName"] ? 1 : -1));
  } else if (selectedOption.value === "По умолчанию") {
    items.value.sort((a, b) => (a["id"] > b["id"] ? 1 : -1));
  } else if (selectedOption.value === "По цене max") {
    items.value.sort((a, b) =>
      parseInt(a["itemPrice"].replace(/[\s.,%]/g, "")) < parseInt(b["itemPrice"].replace(/[\s.,%]/g, "")) ? 1 : -1
    );
  } else if (selectedOption.value === "По цене min") {
    items.value.sort((a, b) =>
      parseInt(a["itemPrice"].replace(/[\s.,%]/g, "")) > parseInt(b["itemPrice"].replace(/[\s.,%]/g, "")) ? 1 : -1
    );
  }
};

watch(
  () => items.value,
  (newValue) => {
    localStorage.setItem("data", JSON.stringify(newValue));
  },
  { deep: true }
);

onMounted(() => {
  if (localStorage.data) {
    items.value = JSON.parse(localStorage.getItem("data"));
  }
});
</script>

<style lang="scss">
@import '../src/styles/App.scss';
</style>
