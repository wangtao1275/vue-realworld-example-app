<template>
  <div class="auth-page">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="text-xs-center">Your Settings</h1>
          <form v-on:submit.prevent="updateSettings();">
            <fieldset>
              <fieldset class="form-group">
                <input type="text" class="form-control form-control-lg" v-model="currentUser.image" placeholder="URL of profile picture" />
              </fieldset>
              <fieldset class="form-group">
                <input type="text" class="form-control form-control-lg" v-model="currentUser.username" placeholder="Your username" />
              </fieldset>
              <fieldset class="form-group">
                <textarea
                  rows="8"
                  class="form-control form-control-lg"
                  v-model="currentUser.bio"
                  placeholder="Short bio about your"
                >
                </textarea>
              </fieldset>
              <fieldset class="form-group">
                <input type="text" class="form-control form-control-lg" v-model="currentUser.email" placeholder="Email" />
              </fieldset>
              <fieldset class="form-group">
                <input type="password" class="form-control form-control-lg" v-model="currentUser.password" placeholder="Password" />
              </fieldset>
              <button class="btn btn-lg btn-primary pull-xs-right">
                Updating Settings
              </button>
            </fieldset>
          </form>
          <hr />
          <button @click="logout" class="btn btn-outline-danger">Or click here to logout.</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { UPDATE_USER, LOGOUT } from '../store/actions.type';
import { mapState, mapGetters } from 'vuex';
  export default {
    name: "RwvSettings",
    methods: {
      updateSettings() {
        this.$store.dispatch(UPDATE_USER, this.currentUser)
          .then(()=> this.$router.push({name: "home"}));
      },
      logout(){
        this.$store.dispatch(LOGOUT).then(()=>{
          this.$router.push({name: "home"})
        })
      }
    },
    computed: {
      ...mapGetters(["currentUser"])
    },
  }
</script>
