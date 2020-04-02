<!-- pages/tag/_id.vue -->

<!-- ここから追加 -->
<template>
  <div>
    <Item 
      v-for="work in works" 
      :key="work.sys.id"
      :work="work"
    />
  </div>
</template>
<!-- ここまで追加 -->

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default {
  asyncData (params) {
    return Promise.all([
      client.getEntries({
        'content_type': 'work',
        'fields.tags.sys.id': params.id,
        order: '-sys.createdAt'
      }),
    ]).then(([works]) => {
      return {
        works: works.items
      }
    }).catch(console.error)
  }
}
</script>