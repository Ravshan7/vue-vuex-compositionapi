<template>
  <div>
    <h3>Создайте новый пост</h3>
    <span>
      <app-field v-model.trim="posts.title" placeholder="Название"/>
      <app-field v-model.trim="posts.body" placeholder="Описание"/>
      <app-button @click="createPost">Добавить</app-button>
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      if (this.posts.title && this.posts.body) {
        this.posts.id = Date.now()
        this.$emit('getFormData', this.posts)
        this.posts = {
          title: '',
          body: ''
        }
      } else {
        alert('Поля не должно быть пустым.')
      }
    }
  }
}
</script>

<style scoped>
div {
  margin-top: 20px;
  background: #fff;
  padding: 30px;
}

div > h3 {
  font-weight: 600;
}

div > span {
  display: grid;
  grid-template-columns: 2fr 2fr 1fr;
  grid-gap: 30px;
  margin-top: 10px;
}

</style>