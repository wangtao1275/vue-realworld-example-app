<template>
  <div class="profile-page">
    <RwvArticleList :favorited="favorited" :items-per-page="5"></RwvArticleList>
  </div>
</template>

<script>
  export default {
    name: "RwvProfileArticles",
    components: {
      RwvArticleList
    },
    computed: {
      favorited() {
        return this.$route.params.username
      }
    },
  }
</script>
