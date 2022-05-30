<template>
  <div class="app">
    <h2> Страница с постами</h2>
    <custom-button
      style="margin: 15px 0"
      @click="showPopup"
    >
      Создать пост
    </custom-button>
    <custom-popup v-model:show="popupVisable">
      <post-form  @create="createPost" />
    </custom-popup>
    <post-list v-if="!loading"
      :posts="posts"
      @remove="removePost"
    />
    <div v-else>Загрузка...</div>
  </div> 
</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'

export default {
  components: {
    PostForm, 
    PostList,
  },
  data() {
    return {
      posts: [],
      popupVisable: false,
      loading: false
    }
  },
  mounted() {
    this.fetchPosts()
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
      this.popupVisable = false
    },
    removePost(post) {
      this.posts = this.posts.filter(({id}) => id !== post.id)
    },
    showPopup() {
      this.popupVisable = true
    },
    async fetchPosts() {
      try {
        this.loading = true
        const res = await fetch('https://jsonplaceholder.typicode.com/posts?_limit=10')
        this.posts = await res.json()
      } catch (error) {
        throw error
      } finally {
        this.loading = false
      }
    },
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}
</style>