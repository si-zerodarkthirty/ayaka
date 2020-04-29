<template>
  <div>
    <div
      v-if="items.length > 0"
      class="flex flex-wrap justify-around w-full"
    >
      <Item
        v-for="item in items" 
        :key="item.sys.id"
        :item="item"
      />
    </div>
    <div v-else>
      <p class="text-center">I've not published any post about "{{ $route.params.keyword }}" yet.</p>
    </div>
  </div>
</template>

<script>
import Item from '@/components/Item'
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  components: {
    Item
  },
  asyncData({params}) {
    return Promise.all([
      client.getEntries({
        'content_type': 'item',
        query: params.keyword,
        order: '-sys.updatedAt'
      })
    ]).then(([items]) => {
      return {
        items: items.items
      }
    }).catch(console.error)
  }
}
</script>