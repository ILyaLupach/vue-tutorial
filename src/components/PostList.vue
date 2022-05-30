<template>
  <div v-if="!!posts.length">
    <h3>Список</h3>
    <post-item 
      v-for="post in posts"
      :post="post"
      :key="post.id"
      @remove="$emit('remove', post)"
    />
  </div>
  <h4 v-else>список постов пуст</h4>
</template>

<script>
import PostItem from '@/components/PostItem'

export default {
  components: {
    PostItem,
  },
  props: {
    posts: {
      type: Array,
      required: true,
    }
  }
}
</script>

<style scoped>

</style>