<template>
  <div class="artile-item">
    <h3>{{ post.title }}</h3>
    <div class="description">{{ post.description }}</div>
    <div class="view-more">
      <a :href="link">view more</a>
    </div>
  </div>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
import Post from '~/models/Post'
export default Vue.extend({
  name: 'PostPreview',
  props: {
    post: {
      type: Object,
      required: true
    } as PropOptions<Post>,
    category: {
      type: String,
      required: true
    }
  },
  computed: {
    link() {
      return `/${this.category}/${this.post.id}`
    }
  }
})
</script>