<template>
  <Header />
  <div class="layout_container">
    <Search />
    <div class="item_container">
      <Item />
      <Item />
      <Item />
      <Item />
      <Item />
      <Item />
    </div>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
import Header from "./components/Header.vue";
import Item from "./components/Item.vue";

export default {
  name: "App",
  components: {
    Search,
    Header,
    Item,
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
</style>
