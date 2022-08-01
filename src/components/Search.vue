<template>
  <div :class="[!validMail() || !validName() ? 'search_error' : 'search']">
    <h5 class="search_title">
      Наименование товара<input
        v-model="productData.productName"
        required
        :class="[validName() ? 'search_input' : 'search_input_error']"
        type="text"
        placeholder="Введите наименование товара"
      />
    </h5>
    <span class="circle_container" v-if="!validName()"
      ><small class="search_error_message"
        >Поле является обязательным</small
      >

      </span
    >
    <h5 class="search_title">
      Описание товара<input
        v-model="productData.productDescription"
        class="search_input_wide"
        type="text"
        placeholder="Введите описание товара"
      />
    </h5>
    <h5 class="search_title">
      Ссылка на изображение товара<input
        v-model="productData.productLink"
        :class="[!!validMail() ? 'search_input' : 'search_input_error']"
        type="text"
        placeholder="Введите ссылку"
      />
    </h5>
    <span v-if="!validMail()"
      ><small class="search_error_message"
        >Поле является обязательным</small
      ></span
    >
    <h5 class="search_title">
      Цена товара
      <input
        @input="productData.productPrice = $event.target.value"
        :value="validPrice(productData.productPrice)"
        class="search_input"
        type="text"
        placeholder="Введите цену"
      />
    </h5>
    <button
      :class="[
        !validMail() || !validName() ? 'search__btn' : 'search__btn_active',
      ]"
    >
      Добавить товар
    </button>
  </div>
</template>

<script setup>
import { ref } from "@vue/runtime-core";

const productData = ref({
  productName: "",
  productDescription: "",
  productLink: "",
  productPrice: "",
});

const validName = () => {
  if (!!productData.value?.productName) return true;
};

const validPrice = (e) => {
  e = e.toString().replace(/[\s.,%]/g, "");
  return e.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ");
};

const validMail = () => {
  return /^https?:\/\/.*\/.*\.(png|gif|webp|jpeg|jpg)\??.*$/gim.test(
    productData.value.productLink
  );
};
</script>

<style lang="scss" scoped>
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
    }
  }

  &_title {
    margin-left: 15px;
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
    width: 268px;
    height: 36px;
    padding: 0 16px;
    /* Darks & Whites / White */
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    border-color: #ff8484;
  }

  &_input::placeholder {
    color: #b4b4b4;
  }

  &_input_wide {
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
