<template>
  <div class="auth-page">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="text-xs-center">Sign up</h1>
          <p class="text-xs-center">
            <router-link :to="{name: 'login'}">
              Have an account?
            </router-link>
          </p>
          <ul v-if="errors" class="error-messages">
            <li v-for="(v, k) in errors" :key="k">{{k}} {{v | error}}</li>
          </ul>
          <form v-on:submit.prevent="onSubmit">
            <fieldset class="form-group">
              <input type="text" class="form-control form-control-lg" v-model="username" placeholder="Username" />
            </fieldset>
            <fieldset class="form-group">
              <input type="text" class="form-control form-control-lg" v-model="email" placeholder="email" />
            </fieldset>
            <fieldset class="form-group">
              <input type="password" class="form-control form-control-lg" v-model="password" placeholder="Password" />
            </fieldset>
            <button class="btn btn-lg btn-primary pull-xs-right">
              Sign up
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { REGISTER } from "../store/actions.type";
import { mapState } from "vuex";
export default {
  name: "RwvRegister",
  data() {
    return {
      username: null,
      email: null,
      password: null
    };
  },
  methods: {
    onSubmit() {
      this.$store
        .dispatch(REGISTER, {
          email: this.email,
          password: this.password,
          username: this.username
        })
        .then(() => this.$router.push({ name: "home" }));
    }
  },
  computed: {
    ...mapState({
      errors: state => state.auth.errors
    })
  }
};
</script>
