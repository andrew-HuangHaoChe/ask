<template>
  <div class="signup-buttons">
    <div id="fb-root"></div>
    <a class="facebook-signup" @click.prevent="login">
    <svg xmlns="http://www.w3.org/2000/svg" width="30px" height="30px" viewBox="0 0 24 24" fill="#3578E5"><path d="M9 8h-3v4h3v12h5v-12h3.642l.358-4h-4v-1.667c0-.955.192-1.333 1.115-1.333h2.885v-5h-3.808c-3.596 0-5.192 1.583-5.192 4.615v3.385z"/></svg>
    </a>
  </div>
</template>
<script>
export default {
  name: 'login_signup_social',
  daata () {
    return {
      profile: {}, // 紀錄登入狀態，當登入時就改變這邊的資料狀態
      authorized: false
    }
  },
  methods: {
    login () {
      const vm = this
      window.FB.login(function (response) {
        console.log('res', response)
        vm.getProfile() // 在使用者登入後call getprofile()取得使用者資訊
      }, {
        scope: 'email, public_profile',
        return_scopes: true
      })
    },
    getProfile () { // 取得登入者資訊的函式；想要取得使用者的 email 或其他資訊，必須使用 Facebook Graph API
      window.FB.api('/me?fields=name,id,email', function (response) {
        console.log('res in graphAPI', response)
      })
    },
    logout () { // 看之後有沒要作社群(FB)登出
      window.FB.logout(function (response) {
        console.log('res when logout', response)
      })
    },
    statusChangeCallback (response) { // 紀錄登入狀態，每當使用者登入的狀態變更時，就會執行這個方法
      const vm = this
      if (response.status === 'connected') {
        vm.authorized = true
        vm.getProfile()
      } else if (response.status === 'not_authorized') {
        vm.authorized = false
      } else {
        vm.authorized = false
      }
    }
  },
  mounted () {
    // const vm =  this
    window.fbAsyncInit = function () {
      window.FB.init({
        appId: '337030707745526',
        cookie: true,
        xfbml: true,
        version: 'v2.9'
      })
      window.FB.AppEvents.logPageView()
      console.log('fbAsyncInit')
      window.FB.getLoginStatus(response => {
        console.log('res', response) // 這裡可以得到 fb 回傳的結果
      })
    }
  }
}
</script>
<style lang="scss">
.signup-buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 73px;
  height: 73px;
  background: #fff;
  border-radius: 50%;
  box-shadow: 0px 2px 4px rgba(155, 155, 155, 0.31963);
}
</style>
