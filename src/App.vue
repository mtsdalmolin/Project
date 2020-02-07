<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About Me</router-link> |
      <router-link to="/contact">Contact Me!</router-link>
    </div>
    <router-view 
      :posts="apiResponse.posts"
      :processDate="processDate"
    />
  </div>
</template>

<script>
export default {
  data () {
    return {
      apiResponse: {}
    } 
  },
  methods: {
    async fetchPosts () {
      return await fetch('https://public-api.wordpress.com/rest/v1/sites/treinamentopipe.home.blog/posts').then(response => response.json())
    },
    processDate (date) {
      let dateInfo = Date(date).split(' ')
      return `${dateInfo[1]} ${dateInfo[2]}, ${dateInfo[3]}`
    }
  },
  async mounted () {
    this.apiResponse = await this.fetchPosts()
  },
}
</script>