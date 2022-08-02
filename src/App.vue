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
      <Item
        v-for="item in filteredItems"
        :key="item.id"
        :item="item"
        @remove="removeItem"
      />
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
      items: [
        {
          itemDescription:
            "Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк",
          itemLink: "",
          itemName: "Наименование товара",
          itemPrice: "10000 руб.",
        },
      ],
      selectedOption: "По умолчанию",
      sortedItems: [],
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
        this.sortedItems = [];
        this.sortedItems = this.items.sort((a, b) =>
          a[this.itemName] < b[this.itemName] ? 1 : -1
        );
        return this.sortedItems;
      } else if (this.selectedOption === "По умолчанию") {
        this.sortedItems = [];
        return this.items;
      } else if (this.selectedOption === "По цене max") {
        this.sortedItems = [];
        this.sortedItems = this.items.sort((a, b) =>
          a[this.itemPrice] > b[this.itemPrice] ? 1 : -1
        );
      } else if (this.selectedOption === "По цене min") {
        this.sortedItems = [];
        this.sortedItems = this.items.sort((a, b) =>
          a[this.itemPrice] < b[this.itemPrice] ? 1 : -1
        );
      }
    },
  },

  computed: {
    filteredItems() {
      if (this.sortedItems.length) return this.sortedItems;
      else return this.items;
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
</style>
