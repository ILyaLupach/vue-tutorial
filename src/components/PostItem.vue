<template>
  <div class="post">
    <div>
      <div><strong>Название: </strong> {{ post.title }}</div>
      <div><strong>Описание: </strong> {{ post.body }}</div>
    </div>
    <div class="post__btns">
      <custom-button @click="$emit('remove', post)">
        Удалить
      </custom-button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    }
  },
}
</script>

<style scoped>
.post {
  padding: 15px;
  margin-top: 15px;
  border: 1px solid teal;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>