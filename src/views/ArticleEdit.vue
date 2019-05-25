<template>
  <div>

  </div>
</template>

<script>
import RwvListErrors from '../components/ListErrors'
import { ARTICLE_RESET_STATE, FETCH_ARTICLE } from '../store/actions.type';
  export default {
    name: "RwvArticleEdit",
    components: {
      RwvListErrors
    },
    props: {
      previousArticle: {
        type: Object,
        required: false
      },
    },
    async beforeRouteUpdate(to, from, next) {
      // Reset state if user goes from /editor/:id to /editor
      // The component is not recreated so we use to hook to reset the state.
      await store.dispatch(ARTICLE_RESET_STATE)
    },

    async beforeRouteEnter (to, from, next) {
      // SO: https://github.com/vuejs/vue-router/issues/1034
      // If we arrive directly to this url, we need to fetch the article
      await store.dispatch(ARTICLE_RESET_STATE)
      if(to.params.slug !== undefined){
        await store.dispatch(FETCH_ARTICLE, to.params.slug, to.params.previousArticle)
      }
      return next();
    },

    async beforeRouteLeave(to, from, next) {
      await store.dispatch(ARTICLE_RESET_STATE)
      next()
    },

  }
</script>
