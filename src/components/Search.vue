<template>
  <div class="search">
    <h5 class="search_title">
      Наименование товара<input
        class="search_input"
        type="text"
        placeholder="Введите наименование товара"
      />
    </h5>
    <h5 class="search_title">
      Описание товара<input
        class="search_input_wide"
        type="text"
        placeholder="Введите описание товара"
      />
    </h5>
    <h5 class="search_title">
      Ссылка на изображение товара<input
        class="search_input"
        type="text"
        placeholder="Введите ссылку"
      />
    </h5>
    <h5 class="search_title">
      Цена товара<input
        class="search_input"
        type="text"
        placeholder="Введите цену"
      />
    </h5>
    <button class="search__btn">Добавить товар</button>
  </div>
</template>

<script></script>

<style lang="scss" scoped>
.search {
  margin-right: 16px;
  width: 332px;
  height: 440px;

  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;

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
  }
}
</style>
