<template>
  <div class="header">
    <h1 class="header_title">Добавление товара</h1>
    <Dropdown />
  </div>
</template>

<script setup>
import Dropdown from "./Dropdown.vue";
import { ref } from "@vue/runtime-core";
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  align-content: space-between;
  justify-content: space-between;

  &_title {
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;

    color: #3f3f3f;
  }
}
</style>
