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
});

const addItem = () => {
  handleChange();
  item.value = {
    itemName: "",
    itemDescription: "",
    itemLink: "",
    itemPrice: "",
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
  return /^https?:\/\/.*\/.*\.(png|gif|webp|jpeg|jpg)\??.*$/gim.test(
    item.value.itemLink
  );
};
</script>

<style lang="scss" scoped>
.circle {
  width: 4px;
  height: 4px;
  background: #ff8484;
  border-radius: 4px;
  margin-top: 16px;

  &_container {
    display: flex;
    margin-left: 16px;
  }
}

.search {
  margin-right: 16px;
  width: 332px;
  height: 440px;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;

  &_error {
    margin-right: 16px;
    width: 332px;
    height: 520px;
    background: #fffefb;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
      0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;

    &_message {
      color: #ff8484;
      margin-left: 16px;
      font-weight: 400;
      font-size: 8px;
      /* identical to box height */
      letter-spacing: -0.02em;
    }
  }

  &_title {
    margin: 16px 0px 4px 0px;
    font-weight: 400;
    font-size: 10px;
    line-height: 13px;
    font-size: 10px;
    line-height: 13px;
    color: #49485e;
    /* identical to box height */
    letter-spacing: -0.02em;
  }

  &_input {
    margin-left: 16px;
    width: 268px;
    height: 36px;
    padding: 0 16px;
    /* Darks & Whites / White */
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    outline: none;
    border: none;
  }

  &_input_error {
    margin-left: 16px;
    width: 268px;
    height: 36px;
    padding: 0 16px;
    /* Darks & Whites / White */
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    border-color: #ff8484;
    outline: none;
  }

  &_input::placeholder {
    color: #b4b4b4;
  }

  &_input_wide {
    margin-left: 16px;
    width: 268px;
    height: 108px;
    padding: 0 16px;
    /* Darks & Whites / White */
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    outline: none;
    border: none;
  }
  &_input_wide::placeholder {
    color: #b4b4b4;
    transform: translateY(-40px);
  }

  &__btn {
    margin: 20px 15px;
    width: 305px;
    height: 36px;
    color: #b4b4b4;
    background: #eeeeee;
    border-radius: 10px;
    outline: none;
    border: none;

    &_active {
      margin: 20px 15px;
      width: 305px;
      height: 36px;
      color: white;
      background: green;
      border-radius: 10px;
      outline: none;
      border: none;
      cursor: pointer;
    }
  }
}
</style>
