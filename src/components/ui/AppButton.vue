<template>
  <button>
    <slot/>
  </button>
</template>

<script>
export default {
  name: 'app-button'
}
</script>

<style scoped>
  button {
    background: #5DBC83;
    outline: none;
    cursor: pointer;
    color: #fff;
    border: none;
    padding: 10px 15px
  }
  button:disabled {
    background: #ccc;
  }
</style>