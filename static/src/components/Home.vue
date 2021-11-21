
<template>
  <div id="home">
    <h1 class="ui header">Login Page</h1>
    <div v-if="!authState?.isAuthenticated">
      <button
          id="login-button"
          class="ui primary button"
          role="button"
          v-on:click="login()"
      >
        Login
      </button>
    </div>

    <div v-if="authState?.isAuthenticated">
      <p>Welcome back, {{claims && claims.name}}!</p>
   </div>
  </div>
</template>

<script>
export default {
  name: 'home',
  data: function () {
    return {
      claims: '',
    }
  },
  created () { this.setup() },
  methods: {
    async setup () {
      if (this.authState?.isAuthenticated) {
        this.claims = await this.$auth.getUser()
      }
    },
    login () {
      this.$auth.signInWithRedirect({ originalUri: '/' })
    }
  }
}
</script>
