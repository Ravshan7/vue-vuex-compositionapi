<template>
  <input :value="modelValue" type="text" @input="changeValue">
</template>

<script>
export default {
  name: 'app-field',
  props: {
    modelValue: {
      type: String
    }
  },
  methods: {
    changeValue(e) {
      this.$emit('update:modelValue', e.target.value)
    }
  }
}
</script>

<style scoped>
  input {
    padding: 10px 15px;
    border: 1px solid #ccc;
    outline: none;
  }
</style>