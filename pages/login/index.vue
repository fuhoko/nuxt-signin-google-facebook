<template>
  <b-container>
    <b-row>
      <b-col class="d-flex align-items-center flex-column mt-5">
        <google-signin></google-signin>
        <facebook-signin
          app-id="614532905843134"
          class="mt-3"
        ></facebook-signin>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import GoogleSignin from '@/components/common/Plugin/GoogleSignin'
import FacebookSignin from '@/components/common/Plugin/FacebookSignin'
export default {
  components: { GoogleSignin, FacebookSignin },
}
</script>
