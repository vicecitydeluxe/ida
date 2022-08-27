<script setup>
const props = defineProps({
  modelValue: {
    type: String,
  },
  options: {
    type: Array,
    default: () => [],
  },
});

const emits = defineEmits(["update:modelValue"]);

const changeOption = (event) => {
  emits("update:modelValue", event.target.value);
};
</script>

<template>
  <select
    class="top__filter-selector"
    v-model="modelValue"
    @change="changeOption"
  >
    <option v-for="option in options" :key="option.value" :value="option.name">
      {{ option.name }}
    </option>
  </select>
</template>

<style lang="scss" scoped>
$font-family: "Source Sans Pro";
$font-style: normal;
$font-weight: 400;
$font-size: 12px;
$line-height: 15px;

.top__filter-selector {
  margin-top: 15px;
  width: 145px;
  height: 36px;
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
  font-size: 12px;
  line-height: 15px;
  color: #b4b4b4;
  padding-left: 16px;
  font-family: $font-family;
  font-style: $font-style;
  font-style: $font-style;
  font-style: $font-style;
  line-height: $line-height;
}
.top__filter-selector:focus {
  outline: 1px solid lightgray;
}
</style>
