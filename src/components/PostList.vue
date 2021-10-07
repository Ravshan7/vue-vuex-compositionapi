<template>
  <div class="main">
    <h3>Список постов</h3>
    <p style="text-align: center; padding-top: 20px; margin-top: 20px; border-top: 1px solid #ececec;"
       v-if="posts === null">
      Загрузка...</p>
    <p style="text-align: center; padding-top: 20px; margin-top: 20px; border-top: 1px solid #ececec;"
       v-else-if="posts.length === 0">Пусто</p>
    <div v-else>
      <transition-group name="post-list">
        <post-item
            v-for="post of posts"
            :post="post"
            @click="$emit('remove', post.id)"
            :key="post.id"
        />
      </transition-group>
    </div>
  </div>
</template>

<script>
import PostItem from "./PostItem";

export default {
  components: {
    PostItem
  },
  props: {
    posts: {
      type: Array || null,
      require: true
    },
  }
}
</script>
<style scoped>
.main {
  margin-top: 30px;
}

.main > h3 {
  font-weight: 600;
}

.post-list-item {
  transition: all .4s ease;
  display: inline-block;
  margin-right: 10px;
}

.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}

.post-list-leave-active {
  position: absolute;
}

.post-list-move {
  transition: transform 0.8s ease;
}
</style>
