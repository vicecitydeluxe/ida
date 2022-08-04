<template>
  <div :class="[!validMail() || !validName() ? 'search_error' : 'search']">
    <div class="circle_container">
      <div class="search_title">Наименование товара</div>
      <div class="circle"></div>
    </div>
    <input
      v-model="item.itemName"
      required
      :class="[validName() ? 'search_input' : 'search_input_error']"
      type="text"
      placeholder="Введите наименование товара"
    />
    <span class="error_title" v-if="!validName()"
      ><small class="search_error_message">Поле является обязательным</small>
    </span>

    <div class="circle_container">
      <div class="search_title">Описание товара</div>
    </div>
    <input
      v-model="item.itemDescription"
      class="search_input_wide"
      type="text"
      placeholder="Введите описание товара"
    />

    <div class="circle_container">
      <div class="search_title">Ссылка на изображение товара</div>
      <div class="circle"></div>
    </div>
    <input
      v-model="item.itemLink"
      :class="[!!validMail() ? 'search_input' : 'search_input_error']"
      type="text"
      placeholder="Введите ссылку"
    />
    <span v-if="!validMail()"
      ><small class="search_error_message"
        >Поле является обязательным</small
      ></span
    >

    <div class="circle_container">
      <div class="search_title">Цена товара</div>
      <div class="circle"></div>
    </div>
    <input
      @input="item.itemPrice = $event.target.value"
      :value="validPrice(item.itemPrice)"
      :class="[!!item?.itemPrice ? 'search_input' : 'search_input_error']"
      type="text"
      placeholder="Введите цену"
    />

    <button
      @click="addItem"
      @create="createItem"
      :disabled="!validMail() || !validName() || !item?.itemPrice"
      :class="[
        !validMail() || !validName() || !item?.itemPrice
          ? 'search__btn'
          : 'search__btn_active',
      ]"
    >
      Добавить товар
    </button>
  </div>
</template>

<script setup>
import { ref } from "@vue/runtime-core";

const emit = defineEmits(["create"]);

const handleChange = () => {
  emit("create", item.value);
};

const item = ref({
  itemName: "",
  itemDescription: "",
  itemLink: "",
  itemPrice: "",
  id: Date.now()
});

const addItem = () => {
  handleChange();
  item.value = {
    itemName: "",
    itemDescription: "",
    itemLink: "",
    itemPrice: "",
    id: Date.now()
  };
};

const validName = () => {
  if (!!item.value?.itemName) return true;
};

const validPrice = (e) => {
  e = e.toString().replace(/[\s.,%]/g, "");
  return e.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ");
};

const validMail = () => {
  return /^http(s)?:\/\/.*\/.*\.(png|gif|webp|jpeg|jpg)\??.*$/gim.test(
    item.value.itemLink
  );
};
</script>

<style lang="scss" scoped>
@import '../styles/Search.scss';
</style>
