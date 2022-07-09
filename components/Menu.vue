<template>
  <div class="menu-wrapper">
    <!-- <nuxt keep-alive /> -->
    <!-- mobile -->
    <div class="d-block d-lg-none menu-horizontal fixed-bottom text-center shadow-lg">
      <div>
        <a-menu v-model="current" mode="horizontal" class="py-3">
          <a-menu-item key="home" style="padding: 0px !important;" @click="$router.push(localeRoute({ name: 'index'}))">
            <a :href="`${domain.main}`">
              <div class="font-weight-normal d-flex flex-column align-items-center justify-content-center">
                <span><svg-icon icon-name="home" style="font-size:1.3em;" /></span>
              </div>
            </a>
          </a-menu-item>
          <a-menu-item key="search" style="padding: 0px !important;">
            <a :href="`${domain.living}/estate`">
              <div class="font-weight-normal d-flex flex-column align-items-center justify-content-center">
                <span><svg-icon icon-name="search" style="font-size:1.2em;" /></span>
              </div>
            </a>
          </a-menu-item>
          <a-menu-item class="px-2">
            <a :href="`${domain.learning}/course`">
              <a-badge>
                <svg-icon icon-name="book" :style="{ fontSize: '1.5rem' }" class="" />
              </a-badge>
            </a>
          </a-menu-item>
          <a-menu-item v-if="user" class="px-2">
            <a :href="`${domain.main}/notify`">
              <a-icon type="bell" :style="{ fontSize: '1.3em' }" />
            </a>
          </a-menu-item>
          <a-menu-item key="building" style="padding: 0px !important;" @click="showDrawers('menuMobile')">
            <div class="font-weight-normal d-flex flex-column align-items-center justify-content-center">
              <span> <a-icon type="menu" style="font-size:1.3em;" /></span>
            </div>
          </a-menu-item>
        </a-menu>
      </div>
    </div>
    <!-- drawer -->
    <a-drawer
      class="drawer"
      height="375"
      placement="bottom"
      :closable="false"
      :visible="showDrawer.menuMobile"
      @close="onClosed('menuMobile')"
    >
      <div slot="title" class="text-center">
        <div>
          <span @click="onClosed('menuMobile')"><a-icon type="minus" style="font-size: 55px;color: #1F3054;" /></span>
        </div>
      </div>
      <div>
        <div class="border-bottom pb-3">
          <a :href="`${domain.living}/estate`" style="color: whitesmoke;">
            <div class="d-flex justify-content-between" @click="onClosed('menuMobile')">
              <div>
                <span><svg-icon icon-name="buildingCity" style="font-size:2em;" /></span>
                <span class="ml-3 text-content">
                  อสังหาฯ
                </span>
              </div>
              <div>
                <span><a-icon type="right" /></span>
              </div>
            </div>
          </a>
        </div>
        <div class="border-bottom py-3">
          <a :href="`${domain.living}/franchise`" style="color: whitesmoke;">
            <div class="d-flex justify-content-between" @click="onClosed('menuMobile')">
              <div>
                <span><svg-icon icon-name="building" style="font-size:2em;" /></span>
                <span class="ml-3 text-content">
                  สาขา
                </span>
              </div>
              <div>
                <span><a-icon type="right" /></span>
              </div>
            </div>
          </a>
        </div>
        <div class="border-bottom py-3">
          <a :href="`${domain.living}/agent`" style="color: whitesmoke;">
            <div class="d-flex justify-content-between" @click="onClosed('menuMobile')">
              <div>
                <span><svg-icon icon-name="person_service" style="font-size:2em;" /></span>
                <span class="ml-3 text-content">
                  ตัวแทน
                </span>
              </div>
              <div>
                <span><a-icon type="right" /></span>
              </div>
            </div>
          </a>
        </div>
        <div class="border-bottom py-3">
          <a :href="`${domain.shopping}/products`" style="color: whitesmoke;">
            <div class="d-flex justify-content-between" @click="onClosed('menuMobile')">
              <div>
                <span><svg-icon icon-name="shopping" style="font-size:2em;" /></span>
                <span class="ml-3 text-content">
                  สินค้าและบริการ
                </span>
              </div>
              <div>
                <span><a-icon type="right" /></span>
              </div>
            </div>
          </a>
        </div>
        <div class="border-bottom py-3">
          <a :href="`${domain.learning}/course`" style="color: whitesmoke;">
            <div class="d-flex justify-content-between" @click="onClosed('menuMobile')">
              <div>
                <span><svg-icon icon-name="book" style="font-size:2em;" /></span>
                <span class="ml-3 text-content">
                  คอร์ส
                </span>
              </div>
              <div>
                <span><a-icon type="right" /></span>
              </div>
            </div>
          </a>
        </div>
        <!-- <div class="pt-3">
          <nuxt-link :to="localePath('job')" style="color: whitesmoke;">
            <div class="d-flex justify-content-between" @click="onClose('menuMobile')">
              <div>
                <span><svg-icon icon-name="bag" style="font-size:2em;" /></span>
                <span class="ml-3 text-content">
                  งาน
                </span>
              </div>
              <div>
                <span><a-icon type="right" /></span>
              </div>
            </div>
          </nuxt-link>
        </div> -->
      </div>
    </a-drawer>
    <a-drawer
      class="drawer-menuAccount"
      placement="left"
      width="85%"
      :closable="false"
      :visible="showDrawer.menuAccount"
      @close="onClosed('menuAccount')"
    >
      <div slot="title">
        <div v-if="user" class="py-3 px-2 border-bottom">
          <div class="d-flex align-items-center">
            <div>
              <a-avatar :size="44" :src="user.profile.profile_image" class="avatar" />
            </div>
            <div class="pl-3">
              <h6 class="m-0">
                {{ user.profile.name }}
              </h6>
              <p class="small m-0" style="color: #465168;">
                {{ user.profile.email }}
              </p>
            </div>
          </div>
        </div>
      </div>
      <div class="menu">
        <a-menu
          class="menu"
          :default-selected-keys="['feed']"
          :default-open-keys="['sub1']"
          mode="inline"
          @click="handleClick"
        >
          <a-menu-item key="feed">
            <svg-icon icon-name="description" style="font-size: 1.5em;" />
            <span class="text-content"><strong>ฟีด</strong></span>
          </a-menu-item>
          <a-menu-item key="profile">
            <svg-icon icon-name="person" style="font-size: 1.5em;" />
            <span class="text-content">โปรไฟล์</span>
          </a-menu-item>
          <a-menu-item key="myEstates">
            <svg-icon icon-name="building" style="font-size: 1.5em;" />
            <span class="text-content">อสังหาของฉัน</span>
          </a-menu-item>
          <a-menu-item key="customerRelations">
            <svg-icon icon-name="book" style="font-size: 1.5em;" />
            <span class="text-content">ลูกค้าสัมพันธ์</span>
          </a-menu-item>
          <a-menu-item key="myCourses">
            <svg-icon icon-name="book" style="font-size: 1.5em;" />
            <span class="text-content">คอร์สเรียนของฉัน</span>
          </a-menu-item>
          <a-menu-item key="myJobs">
            <svg-icon icon-name="bag" style="font-size: 1.5em;" />
            <span class="text-content">งานที่สมัคร</span>
          </a-menu-item>
          <a-menu-item key="myOrders">
            <svg-icon icon-name="orders" style="font-size: 1.5em;" />
            <span class="text-content">คำสั่งซื้อ</span>
          </a-menu-item>
          <a-menu-item key="favorite">
            <svg-icon icon-name="favorite" style="font-size: 1.5em;" />
            <span class="text-content">รายการโปรด</span>
          </a-menu-item>
          <a-menu-item key="setting">
            <svg-icon icon-name="gear" style="font-size: 1.5em;" />
            <span class="text-content">ตั้งค่าและความเป็นส่วนตัว</span>
          </a-menu-item>
          <a-menu-item @click="logout">
            <a-icon type="poweroff" style="font-size: 1.4em;" />
            <span class="text-content"> ออกจากระบบ</span>
          </a-menu-item>
        </a-menu>
      </div>
    </a-drawer>
    <!-- drawer -->
    <!-- mobile -->

    <!-- desktop -->
    <div class="d-none d-lg-block bg fixed-top text-center shadow-sm py-2">
      <div class="container">
        <div class="d-flex align-items-center justify-content-between  menu-submenu">
          <div class="input-search">
            <a :href="`${domain.main}`">
              <logo />
            </a>
          </div>
          <a-menu v-model="redirect" mode="horizontal" class="bg border-0 menu-submenu">
            <a-menu-item>
              <a :href="`${domain.living}/estate`">
                <span class="text-content">อสังหาฯ</span>
              </a>
            </a-menu-item>
            <a-menu-item>
              <a :href="`${domain.living}/franchise`">
                <span class="text-content">แฟรนไชส์</span>
              </a>
            </a-menu-item>
            <a-menu-item>
              <a :href="`${domain.living}/agent`">
                <span class="text-content">ตัวแทน</span>
              </a>
            </a-menu-item>
            <a-menu-item>
              <a :href="`${domain.learning}/course`">
                <span class="text-content">หลักสูตร</span>
              </a>
            </a-menu-item>
            <a-menu-item>
              <div class="text-white">
                <span class="text-white cursor-pointer hover-this-text" @click="$router.push(localeRoute({ name: 'jobs'}))">งาน</span>
              </div>
            </a-menu-item>
            <a-menu-item>
              <a :href="`${domain.shopping}/products`">
                <span class="text-content">สินค้าและบริการ</span>
              </a>
            </a-menu-item>
            <a-menu-item class="d-none d-xxl-block">
              <strong class="text-edit">|</strong>
            </a-menu-item>
            <a-menu-item v-if="!user" :key="`${domain.main}/login`" class="padding-menu">
              <a :href="`${domain.main}/login`">
                <span class="text-content" style="padding: 0 20px;">เข้าสู่ระบบ</span>
              </a>
            </a-menu-item>
            <a-menu-item v-if="!user" key="6" class="padding-menu">
              <a-button class="button-color" shape="round" :href="`${domain.main}/register`">
                <span class="text-content" style="padding: 0 20px;">ลงทะเบียน</span>
              </a-button>
            </a-menu-item>
            <a-sub-menu v-if="user" class="badge-dot">
              <span
                slot="title"
              >
                <!-- :dot="notify&&notify.length?true:false" -->
                <a-badge :count="notify.length">
                  <a-icon type="bell" theme="filled" :style="{ fontSize: '22px', color:'white' }" />
                </a-badge>
              </span>
              <a-menu-item-group style="background-color: #1a2741; color: #fff;">
                <section slot="title" class="d-flex justify-content-between">
                  <div class="d-flex">
                    <h5 class="">
                      การแจ้งเตือน
                    </h5>
                    <a-button type="link" class="pl-2 d-flex align-items-start" style="color: #006697;" :href="`${domain.main}/notify`">
                      <span class="small text-white">ดูทั้งหมด</span>
                      <span class="small lr-1"><a-icon style="color: #006697;" type="arrow-right" /></span>
                    </a-button>
                  </div>
                  <div>
                    <a-icon :style="{ fontSize: '16px', color:'white' }" type="setting" theme="filled" />
                  </div>
                </section>
                <!-- <section slot="title" class="">
                  <div>
                    <div class="d-flex justify-content-between py-3">
                      <div class="">
                        <a-radio-group v-model="modalType" @change="onChangeType">
                          <a-radio-button class="ml-3" value="all">
                            ทั้งหมด
                          </a-radio-button>
                          <a-radio-button v-for="item, index in totalNotify" :key="index" class="ml-3" :value="item.group_code">
                            {{ item.group_name }}({{ item.total }})
                          </a-radio-button>
                        </a-radio-group>
                      </div>
                    </div>
                  </div>
                </section> -->
              </a-menu-item-group>
              <!-- <div v-if="notify"> -->
              <a-menu-item-group v-if="notify_important && notify_important.length" class="menu-submenu" style="background-color: #1a2741; color: #fff;height: 100%;">
                <div slot="title">
                  <p class="text-white">
                    สำคัญ
                  </p>
                </div>
                <a-menu-item v-for="item, index in notify_important" :key="index" style="background-color: #1a2741; color: #fff;height: 100%;cursor: pointer!important;" @click="readNotify(item)">
                  <div class="d-flex justify-content-start mb-3">
                    <div>
                      <div>
                        <a-badge>
                          <a-avatar style="background-color: #c13647;" :size="52">
                            <a-icon type="solution" style="font-size:1.2em !important;color: whitesmoke;" />
                          </a-avatar>
                        </a-badge>
                      </div>
                    </div>
                    <div class="ml-5 small">
                      <div>
                        <h6 class="m-0">
                          {{ item.title }}
                        </h6>
                      </div>
                      <div>
                        <p class="">
                          {{ item.time }}
                        </p>
                      </div>
                      <!-- <a-button>
                        <span class="px-3">ต่อสัญญา</span>
                      </a-button> -->
                    </div>
                  </div>
                </a-menu-item>
              </a-menu-item-group>
              <a-menu-item-group v-if="notify_today && notify_today.length" class="menu-submenu" style="background-color: #1a2741; color: #fff;height: 100%;">
                <div slot="title">
                  <p class="text-white">
                    วันนี้
                  </p>
                </div>
                <a-menu-item v-for="item, index in notify_today" :key="index" style="background-color: #1a2741; color: #fff;height: 100%;" @click="readNotify(item)">
                  <div class="d-flex justify-content-start mb-3">
                    <div>
                      <a-badge>
                        <a-avatar :size="54" :src="item.image" />
                        <div slot="count">
                          <a-button size="small" shape="circle" style="background-color: #006697;margin-right: 20px; margin-top: 90px;">
                            <div v-if="item.type =='social'">
                              <svg-icon :icon-name="item.mode=='comment'?'chat': item.mode=='reply'?'repeat': item.mode=='like'? 'favorite' : item.mode=='contact'? 'person_add':'chat'" style="font-size:1.2em !important;color: whitesmoke;" />
                            </div>
                            <div v-else-if="item.type =='estate'">
                              <svg-icon :icon-name="item.mode=='comment'?'chat': item.mode=='reply'?'repeat': item.mode=='like'? 'building' : item.mode=='contact'? 'person_add':'chat'" style="font-size:1.2em !important;color: whitesmoke;" />
                            </div>
                            <div v-else>
                              <svg-icon :icon-name="item.mode=='comment'?'chat': item.mode=='reply'?'repeat': item.mode=='like'? 'favorite' : item.mode=='contact'? 'person_add':'chat'" style="font-size:1.2em !important;color: whitesmoke;" />
                            </div>
                          </a-button>
                        </div>
                      </a-badge>
                    </div>
                    <div class="ml-5">
                      <div>
                        <h6 class="m-0">
                          {{ item.title }}
                        </h6>
                      </div>
                      <div>
                        <p class="">
                          {{ item.time }}
                        </p>
                      </div>
                    </div>
                  </div>
                </a-menu-item>
              </a-menu-item-group>
              <!-- </div> -->
              <!-- <div v-else> -->
              <a-menu-item-group v-if="!notify.length" style="background-color: #1a2741;">
                <div slot="title" class="d-flex justify-content-center">
                  <div>
                    <h5 style="color: #566178; min-width: 300px !important;" class="text-center">
                      - ยังไม่มีการแจ้งเตือน -
                    </h5>
                  </div>
                </div>
              </a-menu-item-group>
              <!-- </div> -->
            </a-sub-menu>
            <a-menu-item v-if="user" class="px-2 badge-dot">
              <!-- <nuxt-link :to="localePath('notify')"> -->
              <a-badge :count="cart_total">
                <a :href="`${domain.checkout}/cart`">
                  <span><svg-icon icon-name="cart" style="font-size:22px;color:#fff;" /></span>
                </a>
                <!-- <a-icon type="bell" :style="{ fontSize: '22px', color:'white' }" /> -->
              </a-badge>
              <!-- </nuxt-link> -->
            </a-menu-item>
            <a-menu-item v-if="user" key="7">
              <!-- <nuxt-link :to="localePath('profile')">
                <a-avatar :src="user.profile.profile_image" class="avatar" />
              </nuxt-link> -->
              <a :href="`${domain.main}/profile`">
                <a-avatar :src="user.profile.profile_image" class="avatar" />
              </a>
            </a-menu-item>
          </a-menu>
        </div>
      </div>
    </div>
    <!-- desktop -->
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
// import MenuNotify from './user/MenuNotify.vue'

export default {
  // components: { MenuNotify },
  props: {
    account: { type: Boolean, required: false, default: () => false },
    personal: { type: Boolean, required: false, default: () => false }
  },
  data () {
    return {
      redirect: null,
      notify_important: null,
      notify_today: null,
      notify_old: null,
      current: [''],
      molId: false,
      lineOA: false,
      value: '',
      showDrawer: {
        menuMobile: false,
        menuAccount: false
      },
      domain: {
        main: null,
        living: null,
        learning: null,
        shopping: null,
        jobs: null,
        checkout: null
      },
      modalType: 'all'
      // cart_total: 0
      // mol_id: null
    }
  },
  computed: {
    ...mapGetters({
      user: 'user/get',
      profile: 'user/profile',
      sso: 'user/sso',
      cart: 'cart/get',
      totalCart: 'cart/total',
      notify: 'user/notify',
      totalNotify: 'user/totalNotify',
      cart_total: 'user/totalProduct'
    })
    // totalCart () {
    //   const sum = this.cart?.reduce((acc, b) => {
    //     return acc + b.cartQty
    //   }, 0)
    //   return sum
    // }
    // availableLocales () {
    //   return this.$i18n.locales.filter(i => i.code !== this.$i18n.locale)
    // }
  },
  watch: {
    $route (to, from) {
      this.setCurrentPath()
    }
  },
  // eslint-disable-next-line vue/order-in-components
  async fetch () {
    if (this.user) {
      await this.$store.dispatch('user/getNotify')
      await this.$store.dispatch('user/getTotalNotify')
      await this.notify_active()
    }

    // if (this.user) {
    //   console.log('this.notify : ', this.notify)
    //   await this.setNotify()
    // }
    // if (this.user) {
  },
  async mounted () {
    console.log('this.$auth.$storage.getCookie', this.$auth.$storage.getCookies())
    this.domain = {
      main: process.env.REDIRECT_MAIN,
      living: process.env.REDIRECT_LIVING,
      learning: process.env.REDIRECT_LEARNING,
      shopping: process.env.REDIRECT_SHOPPING,
      jobs: process.env.REDIRECT_JOBS,
      checkout: process.env.REDIRECT_CHECKOUT
    }
    console.log('domain : ', this.domain)
    console.log('process.env.REDIRECT_MAIN : ', `${process.env.REDIRECT_MAIN}`)
    const logged = await this.$auth.$storage.getCookie('logged')
    if (logged === 1) {
      await this.$store.dispatch('user/getProfile')
      if (this.user) {
        await this.setNotify()
        await this.$store.dispatch('user/getCart')
      }
    }
  },
  methods: {
    async onChangeType (e) {
      if (this.modalType === 'all') {
        await this.$store.dispatch('user/getNotify')
      } else {
        await this.$store.dispatch('user/getNotify', this.modalType)
      }
      this.notify_active()
    },
    async notify_active () {
      this.notify_important = await this.notify.filter((res) => {
        const result = res.type === 'contact'
        return result
      }
      )
      this.notify_today = await this.notify.filter((res) => {
        const result = res.type === 'today'
        return result
      }
      )
      this.notify_old = await this.notify.filter((res) => {
        const result = res.type === 'day_before'
        return result
      }
      )
    },
    handleRedirect (e) {
      console.log('handleRedirect : ', e)
    },
    async setCart () {
      let cart_token = await this.$auth.$storage.getCookie('_rc.-cart')
      console.log('cart_token')
      console.log('getCookie +_+ ', this.$auth.$storage.getCookie)
      if (!cart_token) {
        cart_token = await this.$axios.$get('/portal/v1/shop/cart/token')
      }
      this.$auth.$storage.setCookie('_rc.-cart', cart_token, {
        path: '/',
        domain: process.env.COOKIES_DOMAIN
        // domain: 'localhost'
      })
      if (cart_token) {
        const payload = {
          cart_token
        }

        const result = await this.$axios.$post(
          '/portal/v1/shop/cart/total',
          payload
        )
        if (result && result.totalProduct) {
          this.cart_total = await result.totalProduct
          const sync_cart_token = this.$axios.$post(
            '/portal/v1/shop/cart/sync',
            payload
          )
          if (sync_cart_token) {
            console.log('sync_cart : ', sync_cart_token)
          }
        }
      }
    },
    async  setNotify () {
      await this.$store.dispatch('user/getNotify')
      // }
      if (this.notify) {
        if (this.notify) {
          for (let i = 0; i < this.notify.length; i++) {
            const cust_id = this.notify[i].cust_id
            this.$socket.emit('enable_notification', { notification_ch_: cust_id })
          }
        }
        this.notify_important = await this.notify.filter((res) => {
          const result = res.type === 'contract'
          return result
        }
        )
        this.notify_today = await this.notify.filter((res) => {
          const result = res.type !== 'contract' && res.date_time < 24
          return result
        }
        )
        this.notify_old = await this.notify.filter((res) => {
          const result = res.date_time > 24
          return result
        }
        )
      }
    },
    readNotify (item) {
      this.$axios.$post(`/portal/v1/notification/${item.message_id}/read`).then(
        (res) => {
          this.$store.dispatch('user/getNotify')
        }
      ).catch((e) => {
        console.log('catch : ', e)
      })
    },
    showDrawers (valueName) {
      this.showDrawer[valueName] = true
    },
    onClosed (valueName) {
      this.showDrawer[valueName] = false
    },
    handleChange (value) {
      return (this.$i18n.setLocale(value))
    },
    setCurrentPath () {
      this.current = this.$nuxt.$route.name ? [`menu-key-${this.$nuxt.$route.name.replace(/(__.*)/, '')}`] : []
    },
    showLogoutConfirm () {
      const _self = this
      this.$confirm({
        centered: true,
        title: this.$t('confirm.logout'),
        okText: this.$t('btn.confirm'),
        cancelText: this.$t('btn.cancel'),
        async onOk () {
          await _self.$store.dispatch('user/logout')
        },
        onCancel () {
        },
        class: 'confirm-logout-wrapper'
      })
    },
    handleClick (e) {
      if (e.key !== '0' && e.key !== '1' && e.key !== '2') {
        this.onClose('menuAccount')
        window.location = `${process.env.REDIRECT_MAIN}/${e}`
      }
    },
    logout (e) {
      this.$store.dispatch('user/logout')
      window.location = process.env.REDIRECT_MAIN
    }
  },
  // eslint-disable-next-line vue/order-in-components
  head () {
    return {
      bodyAttrs: {
        class: ['bg']
      }
    }
  }
}
</script>

<style scoped lang="scss">
@import 'bootstrap/scss/bootstrap-grid';
.ant-menu-item .anticon, .ant-menu-submenu-title .anticon {
    min-width: 14px;
    margin-right: 0px !important;
    font-size: 14px;
    transition: font-size 0.15s cubic-bezier(0.215, 0.61, 0.355, 1), margin 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
}
.menu-wrapper{
  @include media-breakpoint-up(lg) {
    height:  57px;
  }
}

.ant-select-selection--single {
    display: table-row;
}

.small {
    font-size: 0.8em !important;
}
.padding-menu {
    padding: 0 10px !important;
}
.input-search >>> .ant-input-affix-wrapper .ant-input {
    position: relative;
    border-radius: 3rem;
    text-align: initial;
}
.ant-input {
    height: 34px !important;
}
.bg{
  background-color: black !important;
}
.menu-horizontal >>> .ant-menu-horizontal{
  border-bottom: 1px solid #001516;
  border-top: 1px solid #006697;
  border-top-left-radius: 1em 1em;
  border-top-right-radius: 1em 1em;
}
/* .menu-horizontal >>> .ant-menu {
  background: black;
} */
@media (min-width: 1400px){
  .container-xxl, .container-xl, .container-lg, .container-md, .container-sm, .container {
    max-width: 1980px;
  }
}
.ant-menu-item, .ant-menu-submenu-title {
    cursor: unset !important;
}
.ant-menu .ant-menu-item .ant-badge .ant-badge-count {
  padding: 0 3px;
  font-size: 8px;
}
.ant-radio-button-wrapper {
    position: unset;
    display: inherit;
    height: 32px;
    margin: 0;
    padding: 0 15px;
    color: #fff;
    line-height: 30px;
    background: #1e2c48;
    border: 1px solid #1e2c48;
    border-top-width: 1.02px;
    border-left: 1px solid #1e2c48;
    cursor: pointer;
    transition: color 0.3s, background 0.3s, border-color 0.3s, box-shadow 0.3s;
}
.ant-radio-button-wrapper-checked:not(.ant-radio-button-wrapper-disabled) {
    z-index: 1;
    color: #fff;
    background: #006697;
    border-color: #006697;
}
.ant-radio-button-wrapper-checked:not(.ant-radio-button-wrapper-disabled):active {
    color: #fff;
    border-color: #1e2c48;
}
.ant-radio-button-wrapper-checked:not(.ant-radio-button-wrapper-disabled):hover {
    color: #fff;
    border-color: #1e2c48;
    background-color: #006697;
}
.ant-radio-button-wrapper:first-child {
    border: 1px solid #1e2c48;
    border-radius: 5px
}
.ant-radio-button-wrapper {
    border: 1px solid #1e2c48;
    border-radius: 5px
}
</style>
<style scoped>
.drawer >>> .ant-drawer-content {
    color: whitesmoke;
    background-color: #141F36 !important;
    border-radius: 30px 30px 0px 0px !important;
}
.drawer >>> .ant-drawer-header {
    background: #141F36;
    color: whitesmoke !important;
    border-bottom: 0px solid #006697;
    padding: 0px;
}
.drawer >>> .ant-menu-submenu > .ant-menu {
    background-color: #1a2741;
    border-radius: 0.3em;
}
.drawer >>> .ant-drawer-body {
    padding-top: 0px;
}
.border-bottom{
    border-bottom: 1px solid #1F3054 !important;
}
.badge-dot >>> .ant-badge-dot {
    margin-top: 3px;
    margin-right: 5px;
}
/* .menu >>>.ant-menu:not(.ant-menu-horizontal) .ant-menu-item-selected {
    background-color: #1a2741 ;
} */
/* .menu-submenu >>> .ant-menu-submenu>.ant-menu {
    background-color: darkgray;
    border-radius: 4px;
} */
/* .menu-submenu >>> .ant-menu:not(.ant-menu-horizontal) .ant-menu-item-selected {
    background-color: transparent !important;
} */
.drawer-menuAccount >>>  .ant-drawer-left.ant-drawer-open .ant-drawer-content-wrapper {
    background-color: #141F36;
}
.drawer-menuAccount >>>  .ant-drawer-header {
    background: #141F36;
    color: whitesmoke !important;
    border-bottom: 0px solid #006697;
}
.drawer-menuAccount >>>.ant-drawer-content {
    color: whitesmoke;
    background-color: #141F36 !important;
}
.drawer-menuAccount >>> .ant-drawer-body {
    padding: 0px !important;
}
/* .menu >>> .ant-menu {
    color: whitesmoke;
    background: transparent !important;
} */
/* .menu >>> .ant-menu:not(.ant-menu-horizontal) .ant-menu-item-selected {
    background-color: transparent !important;
    padding-left: 24px !important;
} */
/* .menu >>> .ant-menu-inline .ant-menu-item {
    padding-left: 24px !important;
} */
.menu >>> .ant-menu-item-selected {
    color: #b6333a;
}
.menu >>> .ant-menu-submenu > .ant-menu {
    background-color: transparent!important;
    border-radius: 0.3em;
}
.menu >>> .ant-menu-inline, .ant-menu-vertical, .ant-menu-vertical-left {
    border-right: 0px solid #e8e8e8;
}
.hover-this-text:hover {
  color: #b6333a !important;
}
</style>
