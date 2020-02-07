<template>
  <div>
    <div class="post-info">
      <span class="post-title">{{ currentPost.title }}</span>
      <template v-if="currentPost.author.login === 'mtsdalmolin'">
        <router-link to="/about">
          <span class="post-author">{{ currentPost.author.name }}</span>
        </router-link>
      </template>
      <span v-else class="post-author">{{ currentPost.author.name }}</span>
      <span class="post-date">{{ Date(currentPost.date) }}</span>
    </div>
    <div class="post-content">
      <div v-html="currentPost.content">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    posts: Array
  },
  computed: {
    currentPost () {
      return this.posts.find(post => post.ID === +this.$route.params.id)
    }
  }
}
</script>

<style scoped>
span {
  display: block;
}

.post-title {
  font-size: 80px;
}
.post-info {
  display: flex-end;
  margin: 10px;
  padding: 5px;
}
</style>