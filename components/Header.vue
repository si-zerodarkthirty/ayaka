<template>
  <header class="fixed p-5 w-full text-center">
    <h1 class="text-xl cursor-pointer" @click="$router.push('/')">codes&nodes.</h1>
    <h2 class="text-xs">Shusuke IOKU; Waseda; <a href="https://twitter.com/o_dark_3o" target="_blank">@o_dark_3o</a>.</h2>
    <input 
      class="appearance-none block w-full bg-transparent border-b border-black py-3 px-4 mx-auto leading-tight focus:outline-none text-center" 
      type="text"
      v-model="search"
      placeholder="Interstate Bargaining, Military Signals"
      @keypress.enter="$router.push('/search/' + search)"
    >
  </header>
</template>

<style lang="stylus" scoped>
input
  width 100%
  max-width 600px
</style>

<script>
export default {
  data() {
    return {
      search: ''
    }
  }
}
</script>