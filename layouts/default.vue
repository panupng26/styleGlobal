<template>
  <div class="layout-wrapper">
    <Menu />
    <Nuxt class="mb-md-0" style="min-height: calc(100vh - 98px)" />
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
    // setLineLogin () {
    // /* eslint-disable no-undef */
    //   liff.init({
    //     liffId: '1655735625-l5W9v2g8'
    //   }).then(() => {
    //   // console.log(test)
    //     if (liff.isLoggedIn()) {
    //       console.log('test_login : ')
    //       console.log('getAccessToken : ', liff.getAccessToken())
    //       const accessToken = liff.getAccessToken()
    //       console.log('accessToken : ', accessToken)
    //       if (accessToken) {
    //         this.loginLine(accessToken)
    //       }
    //     }
    //     // else {
    //     //   liff.login()
    //     //   console.log('Not_Login >>>>>> ')
    //     // }
    //   })
    // },
    // async loginLine (accessToken) {
    //   const payload = {
    //     // social_type: 'line',
    //     token: accessToken
    //   }
    //   console.log('payload : ', payload)
    //   const result = await this.$axios.$post('/v1/line-login', payload)
    //   console.log('result : ', JSON.stringify(result))
    //   console.log('result.logged : ', result.logged)
    //   if (result && result.logged) {
    //     alert(`redirect_page : ${result.redirect_page}`)
    //     this.$store.dispatch('user/getProfile')
    //     const redirect_page = result.redirect_page
    //     const mol_id = result.mol_id
    //     console.log('const redirect_page : ', redirect_page)
    //     // return this.redirect(redirect_page, mol_id)
    //     if (liff.isInClient()) {
    //       return this.redirect(redirect_page, mol_id)
    //     }
    //   }
    //   this.$notification.error({
    //     message: 'Cannot Login',
    //     description: `${result.error[0].message}`,
    //     onClose: () => {
    //       this.isLoading = false
    //     }
    //   })
    // },
    // redirect (redirect_page, mol_id) {
    //   if (redirect_page == null || redirect_page === undefined) {
    //     return this.$router.push(this.localeRoute({ name: 'jobs' }))
    //   }
    //   if (redirect_page === 'recruit') {
    //     return this.$router.push(this.localeRoute({ name: 'recruit-id', params: { id: mol_id } }))
    //   }
    //   return this.$router.push(this.localeRoute({ name: redirect_page }))
    // }
  }
}
</script>

<style>
/*html {
  font-family:
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}*/
</style>
