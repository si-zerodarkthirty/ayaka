<template>
  <div>
    <h1 class="mt-8 ml-5 text-3xl">{{ item.fields.title }}</h1>
    <p class="ml-5 text-xs">{{ item.sys.updatedAt.slice(0,10) }}</p>
    <div
      v-if="item.fields.content"
      class="content leading-loose my-12"
      v-html="$md.render(item.fields.content)"
    ></div>
    <div 
      class="coverToc fixed top-0 bottom-0 left-0 right-0 z-20" 
      style="background: rgba(255,255,255,.9)"
      @click="removeToc"
    ></div>
    <div class="btn cursor-pointer" @click="drawToc">
      <img src="../../static/bars-solid.svg" alt="">
    </div>
  </div>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  asyncData({params}) {
    return Promise.all([
      client.getEntries({
        'content_type': 'item',
        'fields.slug': params.slug
      })
    ]).then(([items]) => {
      return {
        item: items.items[0]
      }
    }).catch(console.error)
  },
  mounted() {
    document.getElementsByTagName('nav')[0].addEventListener('click', this.removeToc)
  },
  methods: {
    drawToc() {
      document.getElementsByTagName('nav')[0].classList.add('shownToc')
      document.getElementsByClassName('coverToc')[0].classList.add('shownCov')
    },
    removeToc() {
      document.getElementsByTagName('nav')[0].classList.remove('shownToc')
      document.getElementsByClassName('coverToc')[0].classList.remove('shownCov')
    }
  }
}
</script>

<style lang="stylus">
.btn
  position fixed
  top 7.5rem
  right 1rem
  border 2px solid black
  border-radius 50%
  padding .5rem
  img
    width 1rem
    height 1rem
.coverToc
  display none
.shownCov
  display block
.content
  .table-of-contents
    position fixed
    top 0
    bottom 0
    left 0
    height 100%
    width 400px
    margin-left -400px
    background white
    padding 2rem 2rem 2rem 0
    box-shadow 3px 0 3px rgba(0,0,0,.05)
    transition all .1s ease-in-out
    z-index 30
    @media (max-width 768px)
      width 80%
      margin-right -80%
    li
      list-style none
  .shownToc
    margin-left 0
  h2
    font-size 1.5rem
    margin 3rem auto .2rem
    padding 0 1rem
    position relative
  h3
    font-size .9rem
    font-weight bold
    margin 1rem 0 .2rem
    padding 0 1rem
  p
    margin 1rem 0
    padding 0 1rem
    line-height 1.5rem
  li
    list-style circle
    margin-left 2.5rem
  pre
    background #eee
    padding 1rem
    margin 1.5rem 0
    code
      background #eee
      color black
  code
    background #eee
    padding .2rem
    border-radius .2rem
    font-size .8rem
  a 
    border-bottom 1px solid black
  img
    border 1px solid #eee
    padding .3rem 0
    width 50%
    margin 1rem 0
    @media(max-width 768px)
      width 100%
</style>
