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

<script>
import Search from "./components/Search.vue";
import Header from "./components/Header.vue";
import Item from "./components/Item.vue";
import Dropdown from "./components/Dropdown.vue";

export default {
  name: "App",
  components: {
    Search,
    Header,
    Item,
    Dropdown,
  },
  data() {
    return {
      items: [],
      selectedOption: "По умолчанию",
      sortOptions: [
        { value: "default", name: "По умолчанию" },
        { value: "priceMax", name: "По цене max" },
        { value: "priceMin", name: "По цене min" },
        { value: "title", name: "По названию" },
      ],
    };
  },
  methods: {
    createItem(item) {
      this.items.push(item);
    },
    removeItem(item) {
      this.items = this.items.filter((p) => p !== item);
    },

    sortByCategory() {
      if (this.selectedOption === "По названию") {
        this.items.sort((a, b) => (a["itemName"] > b["itemName"] ? 1 : -1));
      } else if (this.selectedOption === "По умолчанию") {
        this.items.sort((a, b) => (a["id"] > b["id"] ? 1 : -1));
      } else if (this.selectedOption === "По цене max") {
        this.items.sort((a, b) =>
          parseInt(a["itemPrice"]) < parseInt(b["itemPrice"]) ? 1 : -1
        );
      } else if (this.selectedOption === "По цене min") {
        this.items.sort((a, b) =>
          parseInt(a["itemPrice"]) > parseInt(b["itemPrice"]) ? 1 : -1
        );
      }
    },
  },
  watch: {
    items: {
      handler(newValue) {
        localStorage.setItem("data", JSON.stringify(newValue));
      },
      deep: true,
    },
  },
  mounted() {
    if (localStorage.data) {
      this.items = JSON.parse(localStorage.getItem("data"));
    }
  },
};
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
