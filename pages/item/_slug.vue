<template>
  <div>
    <h2 class="mt-8 text-2xl text-center">{{ item.fields.title }}</h2>
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
  h3
    font-size 1.2rem
    font-weight bold
    margin 2rem 0 .5rem
  pre
    font-size .9rem
    background #eee
    padding 1rem
    margin 0 -0.5rem
    code
      background #eee
      color black
  code
    background #eee
    padding .2rem
    border-radius .2rem
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
