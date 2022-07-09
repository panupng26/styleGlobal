<template>
  <div class="layout-wrapper">
    <Menu :account="check=true" />
    <Nuxt class="mb-5 mb-md-0 pt-lg-5" style="min-height: calc(100vh - 98px)" />
    <Footer class="d-none d-lg-flex" />
  </div>
</template>

<script>
import { mapState } from 'vuex'
// import liff from '@line/liff'
export default {
  computed: {
    ...mapState({
      accessToken: state => state.accessToken
      // to access local state with `this`, a normal function must be used
      /* countPlusLocalState (state) {
        return state.count + this.localCount
      } */
    })
  },
  async mounted () {
    // eslint-disable-next-line nuxt/no-env-in-hooks
    if (process.browser) {
      // if (!this.accessToken) {
      this.current_token = await this.$auth.$storage.getCookie('current_token') || null
      if (!this.current_token) {
        this.$store.dispatch('getAPIAccessToken')
      } else {
        const accessToken = this.current_token
        await this.$axios.setToken(`${accessToken}`)
        this.$store.commit('setAccessToken', accessToken)
      }
      // }
    }
    if (this.$auth.$storage.getCookie('logged') === 1) {
      if (!this.user) {
        await this.$store.dispatch('user/getProfile')
      }
    }
    if (this.user) {
      // await this.setRole()
      // if (!this.notify.length) {
      //   await this.$store.dispatch('user/getNotify')
      // }
    }
  },
  methods: {
    async setAPIAccess () {
      let accessToken = this.$auth.$storage.getLocalStorage('_token.local')
      if (!accessToken) {
        const { data } = await this.$auth.loginWith('local')
        accessToken = data.access_token
      }
      console.log('APIAccesstoken', accessToken)
      this.$store.commit('setAccessToken', accessToken)
      await this.$axios.setToken(`${accessToken}`)
    }
  }
}
</script>

<style>
</style>
