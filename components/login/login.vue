<template>
  <div class=" d-flex flex-column h-screen">
    <div class="page page-center sign-in z-1" :style="{backgroundImage: `url(${bgImage})`}">
      <div class="sign-in-bg"></div>
      <div class="container container-tight py-4">
        <div class="text-center mb-4 z-50 relative  ">
          <nuxt-link to="/" class="navbar-brand navbar-brand-autodark">
            <nuxt-icon name="wlogo/gulce" class="gulce-logo gulce-home-logo"/>
          </nuxt-link>
        </div>
        <div class="card card-md">
          <div class="card-body">
            <h2 class="h2 text-center mb-4">Giriş Yap</h2>
            <LoginForm />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import LoginForm from '@/components/login/loginForm.vue'
import bgImage from '@/assets/img/bg-sign-in.jpg'
export default {
  data() {
    return {
      bgImage
    }
  }
}
</script>

<style lang="scss" scoped>

</style>