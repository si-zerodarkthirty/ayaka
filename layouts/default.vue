<template>
  <div>
    <Header />
    <main class="mx-auto">
      <nuxt />
    </main>
  </div>
</template>

<script>
import Header from '@/components/Header'
export default {
  components: {
    Header
  }
}
</script>

<style lang="stylus">
html
  font-family 'Ubuntu', 'Yu Gothic', 'YuGothic', sans-serif
  font-size 14px
  word-spacing 1px
  -ms-text-size-adjust 100%
  -webkit-text-size-adjust 100%
  -moz-osx-font-smoothing grayscale
  -webkit-font-smoothing antialiased
  box-sizing border-box
main
  width 100%
  padding-top 6.8rem
</style>
