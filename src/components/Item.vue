<template>
  <div class="item">
    <img @click="removeItem" class="item_remove" :src="svg" />
    <div class="item_wrapper">
      <img class="item_card" :src="item.itemLink || require(`../assets/card.jpg`)" />
    </div>
    <div class="item_info">
      <h1 class="item_title">{{ item.itemName }}</h1>
      <p class="item_description">
        {{ item.itemDescription }}
      </p>
      <strong class="item_price">{{ validPrice(item.itemPrice) }} руб.</strong>
    </div>
  </div>
</template>

<script>
export default {
  name: "Item",
  data() {
    return {
      svg: require("../assets/trash_btn.svg"),
    };
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  methods: {
    removeItem() {
      this.$emit("remove", this.item);
    },
    validPrice(e) {
      e = e.toString().replace(/[\s.,%]/g, "");
      return e.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ")
    }
  },
};
</script>

<style lang="scss" scoped>
@import '../styles/Item.scss';
</style>
