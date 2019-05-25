<template>
  <div class="article-page">
    <div class="banner">
      <div class="container">
        <h1>{{article.title}}</h1>

      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import { RwvArticleMeta } from '../components/ArticleMeta'
import { RwvComment} from '../components/Comment'
import { RwvCommentEditor } from '../components/CommentEditor'
import { RwvTag } from '../components/VTag'
import { FETCH_ARTICLE, FETCH_COMMENTS } from '../store/actions.type';
import marked from 'marked'
import store from '@/store'
  export default {
    name: "rwv-article",
    props: {
      slug: {
        type: String,
        required: true
      },
    },
    components: {
      RwvArticleMeta,
      RwvComment,
      RwvCommentEditor,
      RwvTag
    },
    beforeEnter: (to, from, next) => {
      Promise.all([
        store.dispatch(FETCH_ARTICLE, to.params.slug),
        store.dispatch(FETCH_COMMENTS, to.params.slug)
      ]).then(() => {
        next();
      })
    },
    computed: {
      ...mapGetters(["article", "currentUser", "comments", "isAuthenticated"])
    },
    methods: {
      parseMarkdown(content) {
        return marked(content);
      }
    },

  }
</script>

