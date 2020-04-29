<template>
  <header 
    class="fixed py-5 px-2 w-full text-center" 
    :class="{ 'hidden': !showNavbar }"
  >
    <h1 class="text-xl cursor-pointer" @click="$router.push('/')">codes&nodes.</h1>
    <h2 class="text-xs">Shusuke IOKU; Waseda; <a href="https://twitter.com/o_dark_3o" target="_blank">@o_dark_3o</a>.</h2>
    <input 
      class="appearance-none block w-full bg-transparent border-b border-black p-3 mx-auto leading-tight focus:outline-none text-center" 
      type="text"
      v-model="search"
      placeholder="Interests: Interstate Bargaining, Military Signals, Causal Inference"
      @keypress.enter="$router.push('/search/' + search)"
    >
  </header>
</template>

<style lang="stylus" scoped>
header
  transform translate3d(0, 0, 0)
  transition 0.1s all ease-out

.hidden
  transform translate3d(0, -100%, 0)
input
  width 100%
  max-width 600px
</style>

<script>
export default {
  data() {
    return {
      search: '',
      showNavbar: true,
      lastScrollPosition: 0
    }
  },
  mounted () {
    window.addEventListener('scroll', this.onScroll)
  },
  beforeDestroy () {
    window.removeEventListener('scroll', this.onScroll)
  },
  methods: {
    onScroll () {
      const currentScrollPosition = window.pageYOffset || document.documentElement.scrollTop
      if (currentScrollPosition < 0) {
        return
      }
      if (Math.abs(currentScrollPosition - this.lastScrollPosition) < 60) {
        return
      }
      this.showNavbar = currentScrollPosition < this.lastScrollPosition
      this.lastScrollPosition = currentScrollPosition
    }
  }
}
</script>