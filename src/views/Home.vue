<template>
  <div class="home">
    <span class="title">Welcome to Mathico's Final Challenge Vue Project</span>
    <div class="content" v-if="this.loading">
      Carregando...
    </div>
    <div class="content" v-else>
      <template v-for="(post, index) in posts.slice(0, numberOfPosts)">
        <div :key="index">
          <span class="post-title">{{ post.title }}</span>
          <span class="pub-date">{{ processDate(post.date) }} in {{ post.categories["Sem categoria"].name }}</span>
          <div v-html="post.excerpt" class="post-excerpt">
          </div>
          <router-link :to="`/post/${post.ID}/${post.slug}`">
            <span class="read-more">Read More</span>
          </router-link>
        </div>
      </template>
      <span class="load-more" @click="loadMorePosts">Load more posts!</span>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      numberOfPosts: 5,
      loading: true
    }
  },
  props: {
    posts: {
      type: Array
    },
    processDate: {
      type: Function
    }
  },
  methods: {
    loadPosts () {
      setTimeout(() => {
          this.loading = false;
      }, 2000)
    },
    loadMorePosts () {
      this.numberOfPosts += 5
    }
  },
  mounted () {
    this.loadPosts()
  }
}
</script>

<style scoped>
.load-more {
  cursor: pointer;
  padding: 10px;
  margin: 10px;
}
.load-more:hover {
  font-weight: bold;
}
span.read-more {
  display: inline-flex;
}
.title {
  text-align: center;
  font-size: 60px;
  font-weight: bold;
}
.content {
  text-align: center;
  font-size: 200%;
}
.content div {
  margin: 15px;
  background-color: azure;
}
</style>