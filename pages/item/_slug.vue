<template>
  <div>
    <h2 class="mt-8 text-3xl text-center">{{ item.fields.title }}</h2>
    <p class="text-center text-xs">{{ item.sys.updatedAt.slice(0,10) }}</p>
    <div
      v-if="item.fields.content"
      class="content leading-loose my-12"
      v-html="$md.render(item.fields.content)"
    ></div>
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
  }
}
</script>

<style lang="stylus">
.content
  .table-of-contents
    li
      list-style none
  h3
    font-size 1.7rem
    margin 5rem auto 1rem
    padding 0 1rem
    text-align center
    position relative
  h4
    font-size 1.3rem
    margin 2rem 0 .5rem
  p
    margin 1rem 0
  li
    list-style circle
    margin-left 2rem
  pre
    background #eee
    padding 1rem
    margin 1.5rem 0
    @media (max-width 590px)
      margin 0 -0.5rem
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
    padding .3rem
    width 50%
    margin 1rem 0
    @media(max-width 650px) {
      width 100%
    }
</style>
