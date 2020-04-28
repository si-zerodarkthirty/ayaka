<template>
  <div>
    <div class="flex flex-wrap justify-around w-full">
      <Item
        v-for="item in items" 
        :key="item.sys.id"
        :item="item"
      />
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
  asyncData() {
    return Promise.all([
      client.getEntries({
        'content_type': 'item',
        order: '-sys.createdAt'
      })
    ]).then(([items]) => {
      return {
        items: items.items
      }
    }).catch(console.error)
  }
}
</script>