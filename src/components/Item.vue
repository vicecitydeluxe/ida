<template>
  <div class="item">
    <img class="item_remove" :src="svg" />
    <div class="item_wrapper">
      <img class="item_card" src="../assets/card.jpg" />
    </div>
    <div class="item_info">
      <h1 class="item_title">Наименование товара</h1>
      <p class="item_description">
        Довольно-таки интересное описание товара в&nbsp;несколько строк.
        Довольно-таки интересное описание товара в&nbsp;несколько строк
      </p>
      <strong class="item_price">10000 руб.</strong>
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
};
</script>

<style lang="scss" scoped>
$text-color: #3f3f3f;

.item {
  position: relative;
  width: 100%;
  max-width: 470px;
  line-height: 1.25;
  color: grey;
  background-color: white;
  border-radius: 0.25rem;
  box-shadow: 0px 20px 30px rgb(0 0 0 / 4%), 0px 6px 10px rgb(0 0 0 / 2%);

  &_remove {
    position: absolute;
    top: -0.5rem;
    right: -0.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 2rem;
    width: 2rem;
    border: none;
    padding: 0;
    cursor: pointer;
    z-index: 1;
    opacity: 0;
    transition: 0.2s opacity ease, 0.2s visibility ease;

    &:hover {
      opacity: 1;
    }
  }

  &_wrapper {
    position: relative;
    flex: 1;
    width: 100%;
    border-top-left-radius: 0.25rem;
    border-top-right-radius: 0.25rem;
    padding-bottom: 60.2409638554%;
    overflow: hidden;
  }

  &_card {
    position: absolute;
    width: 100%;
    height: 100%;
    object-fit: contain;
  }

  &_info {
    padding: 1rem;
    padding-bottom: 1.5rem;
  }

  &_title {
    color: $text-color;
    font-size: 1.25rem;
    font-weight: 600;
    line-height: 1.25;
    margin: 0;
    margin-bottom: 1rem;
  }

  &_description {
    color: $text-color;
    font-weight: 400;
    line-height: 1.25;
    margin: 0;
    margin-bottom: 2rem;
  }

  &_price {
    color: $text-color;
    font-size: 1.5rem;
    font-weight: 600;
  }
}
</style>
