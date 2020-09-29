<template>
  <button class="button-login-facebook" @click="logInWithFacebook">
    <font-awesome-icon :icon="['fab', 'facebook-f']" class="mr-1" />
    {{ loginLabel }}
  </button>
</template>

<script>
export default {
  props: {
    appId: {
      type: String,
      required: true,
    },
    version: {
      type: String,
      default: 'v8.0',
    },
    loginLabel: {
      type: String,
      default: 'Log in to Facebook',
    },
  },
  async created() {
    await this.loadFacebookSDK(document, 'script', 'facebook-jssdk')
    await this.initFacebook()
  },
  methods: {
    initFacebook() {
      window.fbAsyncInit = async () => {
        await window.FB.init({
          appId: this.appId,
          cookie: true,
          version: 'v8.0',
          xfbml: true,
        })
      }
    },
    loadFacebookSDK(d, s, id) {
      const fjs = d.getElementsByTagName(s)[0]
      if (d.getElementById(id)) {
        return
      }
      const js = d.createElement(s)
      js.id = id
      js.src = 'https://connect.facebook.net/en_US/sdk.js'
      fjs.parentNode.insertBefore(js, fjs)
    },
    logInWithFacebook() {
      window.FB.login((response) => {
        if (response.authResponse) {
          this.$emit('getToken', response.authResponse.accessToken)
        }
      })
      return false
    },
  },
}
</script>

<style scoped>
.button-login-facebook {
  border: none;
  color: #fff;
  line-height: 34px;
  min-width: 225px;
  background-image: linear-gradient(#4c69ba, #3b55a0);
}
</style>
