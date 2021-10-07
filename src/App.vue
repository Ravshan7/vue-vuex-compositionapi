<template>
  <div class="container app">
    <span>
      <h3>Создать новый пост</h3>
      <div style="display: flex; align-items: center; grid-gap: 30px">
        <app-button :disabled="!posts" @click="isModal = !isModal">Создать</app-button>
        <app-select v-model="selectValue" :options="selectData"/>
        <app-field v-model="searchValue" placeholder="Поиск"/>
      </div>
    </span>
    <app-modal :isShowHide="isModal" @hideModal="isModal = false">
      <form-post @getFormData="createPost"/>
    </app-modal>
    <post-list :posts="searchPost" @remove="deletePost"/>
    <div class="pagination">
      <button
          v-for="buttonPage of pagination.buttons"
          :class="{'current-page': pagination.page === +buttonPage}"
          @click="pagination.page = +buttonPage"
      >
        {{ buttonPage }}
      </button>
    </div>
  </div>
</template>

<script>
import FormPost from "./components/FormPost";
import PostList from "./components/PostList";
import axios from 'axios'

export default {
  components: {
    FormPost,
    PostList
  },
  data() {
    return {
      posts: null,
      isModal: false,
      selectValue: '',
      selectData: [
        {value: 'title', name: 'По названию'},
        {value: 'body', name: 'По описанию'}
      ],
      searchValue: '',
      pagination: {
        count: 10,
        page: 1,
        buttons: []
      }
    }
  },
  methods: {
    createPost(post) {
      this.posts = [post, ...this.posts]
      this.isModal = false
    },
    deletePost(id) {
      this.posts = this.posts.filter(post => post.id !== id)
    },
    async getPosts() {
      this.posts = null
      try {
        const {
          data,
          headers
        } = await axios.get(`https://jsonplaceholder.typicode.com/posts?_limit=${this.pagination.count}&_page=${this.pagination.page}`)
        data.forEach(el => {
          delete el.userId
        })
        this.posts = data
        this.pagination.buttons = new Array(Math.ceil(headers['x-total-count'] / this.pagination.count)).fill('').map((el, idx) => idx + 1)
      } catch (e) {
        console.log(e.error)
      }
    },
  },

  mounted() { // Работает после рендеринга дом дерево как componentDidMount
    this.getPosts()
  },

  watch: { // Watch наблюдает, если что-то из переданных методов и переменных изменяется, тогда он работает.
    // selectValue(value) {
    //   this.posts.sort((post1, post2) => {
    //     return post1[value].localeCompare(post2[value])
    //   })
    // }
    'pagination.page'(value) {
      this.getPosts()
    }
  },

  computed: { // Работает как watch но вызывает один раз, кэширует и наблюдает, но должен что-то вернуть
    sortPosts() {
      if (this.posts) {
        return [...this.posts]?.sort((a, b) => {
          return a[this.selectValue]?.localeCompare(b[this.selectValue])
        })
      }
      return null
    },
    searchPost() {
      if (this.sortPosts) {
        return this.sortPosts.filter(post => post.title.toLowerCase().includes(this.searchValue.toLowerCase()))
      }
      return null
    }
  }

}


</script>

<style scoped>
span {
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid #ccc;
  padding-bottom: 20px;
}

span > h3 {
  font-weight: 600;
}

.pagination {
  margin-top: 10px;
}

.pagination button {
  padding: 5px 10px;
  margin: 5px 10px;
  cursor: pointer;
  border: none;
  border-radius: 5px
}

.pagination .current-page {
  background: green;
  color: #fff;
}
</style>
