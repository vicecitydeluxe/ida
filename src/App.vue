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
          v-for="(item, index) in items"
          :key="index"
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
      parseInt(a["itemPrice"]) < parseInt(b["itemPrice"]) ? 1 : -1
    );
  } else if (selectedOption.value === "По цене min") {
    items.value.sort((a, b) =>
      parseInt(a["itemPrice"]) > parseInt(b["itemPrice"]) ? 1 : -1
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
html,
body {
  background-color: #fffefb;
}

#app {
  font-family: "Source Sans Pro";
  font-style: normal;
  margin: 0 32px;
}

.layout_container {
  display: flex;
}

.item_container {
  grid-gap: 16px;
  display: grid;
  grid-auto-flow: row;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, 1fr);
}

.header {
  display: flex;
  align-content: space-between;
  justify-content: space-between;
}

.item-list-enter-active {
  animation: item-list-in 0.5s;
}
.item-list-leave-active {
  animation: item-list-in 0.5s alternate-reverse;
}
@keyframes item-list-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}
</style>
