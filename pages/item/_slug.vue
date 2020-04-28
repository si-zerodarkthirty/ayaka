<template>
  <div>
    <h2 class="mt-8 font-bold text-2xl text-center">{{ item.fields.title }}</h2>
    <div
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
    margin 1.5rem 0 1rem
  pre
    font-size .9rem
    background #eee
    padding 1rem
    code
      background #eee
      color black
  a 
    border-bottom 1px solid black
</style>
