<template>
  <div class="main" v-if="isShowHide" @click="$emit('hideModal', false)">
    <div @click.stop>
      <slot/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app-modal',
  props: {
    isShowHide: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped>
.main {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.56);
}
</style>