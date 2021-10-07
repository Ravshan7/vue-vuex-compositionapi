<template>
  <div>
      <span>
      <h4>{{ post.title }}</h4>
      <p>{{ post.body }}</p>
    </span>
    <app-button style="background: #B9000D">Удалть</app-button>
  </div>
</template>

<script>
import AppButton from "./ui/AppButton";

export default {
  components: {AppButton},
  props: {
    post: {
      type: Object,
      require: true
    }
  }
}
</script>

<style scoped>
div {
  border: 2px solid #5DBC83;
  margin-top: 10px;
  padding: 10px 15px;
  display: grid;
  grid-template-columns: 1fr auto;
  grid-gap: 30px;
  align-items: center;
  background: #fff;
}

div > span > h4 {
  font-weight: 600;
  font-size: 14px;
}

div > span > p {
  margin-top: 10px;
}
</style>
