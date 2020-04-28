<template>
  <div>
    <Header />
    <main class="pt-24 px-3 mx-auto">
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
@import url('https://fonts.googleapis.com/css2?family=Quicksand&display=swap')
html
  font-family 'Quicksand', 'Yu Gothic', 'YuGothic', sans-serif
  font-size 14px
  word-spacing 1px
  -ms-text-size-adjust 100%
  -webkit-text-size-adjust 100%
  -moz-osx-font-smoothing grayscale
  -webkit-font-smoothing antialiased
  box-sizing border-box
main
  width 100%
  max-width 600px
</style>
