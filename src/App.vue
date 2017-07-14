<template>
  <div id="app">
    <div v-for="author in authors">
      <img width="100" :src="author.img">
      <h1>{{ author.name }}</h1>
      <p>{{ author.bio }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      authors: []
    }
  },
  mounted () {
    const self = this
    const authors = ['halfeld', 'gouveaheitor', 'rodrigoterrongit']

    authors.map((author) => {
      self.loadAuthors(author)
        .then(({data}) => data)
        .then((res) => {
          self.authors.push({
            name: res.name,
            bio: res.bio,
            img: res.avatar_url
          })
        })
        .catch(console.log)
    })
  },
  methods: {
    loadAuthors (author) {
      return this.$http.get(`https://api.github.com/users/${author}`)
    }
  }
}
</script>

<style>
</style>
