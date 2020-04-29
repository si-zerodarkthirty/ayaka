<template>
  <header 
    class="fixed py-5 px-2 w-full text-center" 
    :class="{ 'hidden': !showNavbar }"
  >
    <h1 class="text-xl cursor-pointer" @click="$router.push('/')">codes&proofs.</h1>
    <a href="https://twitter.com/o_dark_3o" target="_blank"><h2 class="text-xs">Shusuke IOKU</h2></a>
    <input 
      class="appearance-none block w-full p-2 mt-1 mx-auto leading-tight focus:outline-none text-center text-xs" 
      type="text"
      v-model="search"
      placeholder="Type any keywords and press enter."
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
  width calc(100% - 1rem)
  max-width calc(600px - 1rem)
  background #eee
  border-radius 1rem
::-webkit-input-placeholder
  color black
:-ms-placeholder
  color black
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