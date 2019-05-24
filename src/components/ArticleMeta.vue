<template>
  <div class="article-meta">
    <router-link :to="{name: 'profile', params: {username: article.author.username }}">
      <img :src="article.author.image" />
    </router-link>
    <div class="info">
      <router-link :to="{name: 'profile', params: {username: article.author.username }}" class="author">
        {{article.author.username}}
      </router-link>
      <span class="date">{{ article.createdAt | date}}</span>
    </div>
    <template v-if="actions">
      <rwv-article-actions
        :article="article"
        :canModify="isCurrentUser()"
      />
    </template>
    <template v-else>
      <button
        class="btn btn-sm pull-xs-right"
        v-if="!actions"
        v-on:click="toggleFvorite"
        :class="{
          'btn-primary': article.favorited,
          'btn-outline-primary': !article.favorited
        }"
      >
        <i class="ion-heart"></i>
        <span class="counter">{{article.favoritesCount}}</span>
      </button>
    </template>
  </div>
</template>

<script>
import RwvArticleActions from "./ArticleActions";
import { mapGetters } from "vuex";
import { FAVORITE_REMOVE, FAVORITE_ADD } from "../store/actions.type";

export default {
  name: "RwvArticleMeta",
  components: {
    RwvArticleActions
  },
  props: {
    article: {
      type: Object,
      required: true
    },
    actions: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  computed: {
    ...mapGetters(["currentUser", "isAuthenticated"])
  },
  methods: {
    isCurrentUser() {
      if (this.currentUser.username && this.article.author.username) {
        return this.currentUser.username === this.article.author.username;
      }
      return false;
    },

    toggleFvorite() {
      if (!this.isAuthenticated) {
        this.$router.push({ name: "login" });
        return;
      }
      const action = this.article.favorited ? FAVORITE_REMOVE : FAVORITE_ADD;
      this.$store.dispatch(action, this.article.slug);
    }
  }
};
</script>
