<script setup>
import { ref, computed } from "@vue/runtime-core";

const emit = defineEmits(["create"]);

const handleChange = () => {
  emit("create", item.value);
};

const item = ref({
  itemName: "",
  itemDescription: "",
  itemLink: "",
  itemPrice: "",
  id: Date.now(),
});

const addItem = () => {
  handleChange();
  item.value = {
    itemName: "",
    itemDescription: "",
    itemLink: "",
    itemPrice: "",
    id: Date.now(),
  };
};

const validName = computed(() => {
  if (!!item.value?.itemName)
    return /^[a-zA-Z0-9А-Яа-я]{3,}$/.test(item.value.itemName);
  else if (item.value.itemName === "") return true;
});

const validPrice = (e) => {
  const patternOnlyNumbers = /[^0-9.]/g
  if (patternOnlyNumbers.test(e) || patternOnlyNumbers.test(item.value.itemPrice)) {
    item.value.itemPrice = item.value.itemPrice.replace(patternOnlyNumbers, '')
    e = e.replace(patternOnlyNumbers, '')
    return e.replace(/\B(?=(\d{3})+(?!\d))/g, " ");
  }
  else {
    e = e.replace(/[\s.,%]/g, "");
    return e.replace(/\B(?=(\d{3})+(?!\d))/g, " ");
  }
}

const validLink = computed(() => {
  if (item.value.itemLink !== "") {
    return /^http(s)?:\/\/.*\/.*\.(png|gif|webp|jpeg|jpg)\??.*$/gim.test(
      item.value.itemLink
    );
  } else return true;
});

const focused = ref(false);

const onFocus = () => {
  focused.value = true;
};

const onBlur = () => {
  focused.value = false;
};
</script>

<template>
  <div :class="[!validLink || !validName ? 'search_error' : 'search']">
    <div class="circle_container">
      <div class="search_title">Наименование товара</div>
      <div class="circle"></div>
    </div>
    <input
      v-model="item.itemName"
      :class="[validName ? 'search_input' : 'search_input_error']"
      type="text"
      placeholder="Введите наименование товара"
    />
    <span class="error_title" v-if="!validName"
      ><small class="search_error_message"
        >Поле является обязательным, введите хотя бы 3 символа</small
      >
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
      :class="[!!validLink ? 'search_input' : 'search_input_error']"
      type="text"
      placeholder="Введите ссылку"
    />
    <span v-if="!validLink"
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
      @focus="onFocus()"
      @blur="onBlur()"
      :value="validPrice(item.itemPrice)"
      class="search_input"
      type="text"
      placeholder="Введите цену"
    />
    <span v-if="!item.itemPrice && focused"
      ><small class="search_error_message"
        >Поле является обязательным (только числа)</small
      ></span
    >
    <button
      @click="addItem"
      @create="createItem"
      :disabled="!item?.itemLink || !validLink || !validName || !item?.itemPrice"
      :class="[
        !item?.itemLink || !validLink || !validName || !item?.itemPrice
          ? 'search__btn'
          : 'search__btn_active',
      ]"
    >
      Добавить товар
    </button>
  </div>
</template>

<style lang="scss" scoped>
@import "../styles/Search.scss";
</style>
