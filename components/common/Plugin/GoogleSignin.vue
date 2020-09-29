<template>
  <div id="g-signin" class="g-signin2"></div>
</template>

<script>
export default {
  props: {
    width: {
      type: Number,
      default: 240,
    },
    height: {
      type: Number,
      default: 50,
    },
    longtitle: {
      type: Boolean,
      default: true,
    },
    theme: {
      type: String,
      default: 'dark',
    },
  },
  mounted() {
    this.renderButton()
  },
  methods: {
    onSuccess(googleUser) {
      this.$emit('onSuccess', googleUser)
    },
    onFailure(error) {
      this.$emit('onFailure', error)
    },
    renderButton() {
      window.onLoadCallback = async () => {
        await window.gapi.signin2.render('g-signin', {
          scope: 'profile email',
          width: this.width,
          height: this.height,
          longtitle: true,
          theme: this.theme,
          onsuccess: this.onSuccess,
          onfailure: this.onFailure,
        })
      }
    },
  },
}
</script>

<style lang="css" scoped></style>
