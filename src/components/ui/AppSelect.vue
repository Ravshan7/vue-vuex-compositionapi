<template>
  <select :value="modelValue" @change="$emit('update:modelValue', $event.target.value)">
    <option disabled value="">Выберите из списка</option>
    <option v-for="option of options" :value="option.value">{{option.name}}</option>
  </select>
</template>

<script>
export default {
  name: "app-select",
  props: {
    modelValue: {
      type: String,
      require: true,
    },
    options: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style scoped>
select {
  padding: 10px 15px;
  outline: none;
}
</style>