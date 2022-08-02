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

<script>
export default {
  props: {
    modelValue: {
      type: String,
    },
    options: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    changeOption(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
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
}
.top__filter-selector:focus {
  outline: 1px solid lightgray;
}
</style>
