<template>
  <div>
    <div class="posts">
      <post-preview v-for="post in postList" :key="post.id" :post="post" :category="category" />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'
import PostPreview from '~/components/PostPreview'

const CATEGORYS = ['news', 'newest', 'ask', 'show', 'jobs']
const getApi = (category: string, pageIndex: number) =>
  `https://api.hnpwa.com/v0/${category}/${pageIndex}.json`

export default Vue.extend({
  async asyncData({ params, res }) {
    const { category } = params
    if (!CATEGORYS.includes(category)) {
      return {}
    }
    const url = getApi(category, 1)
    const resp = await axios.get(url)
    return { postList: resp.data, category }
  },
  components: {
    PostPreview
  },
  data() {
    return {
      pageIndex: 1,
      category: '',
      postList: []
    }
  }
})
</script>