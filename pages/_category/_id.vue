<template>
  <div>
    <div class="post">
      <h1>{{artile.title}}</h1>

      <div>{{artile.content}}</div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'

const getApi = (id: string) => `https://api.hnpwa.com/v0/item/${id}.json`

export interface Article {
  id: number
  title: string
  points: number | null
  user: string | null
  time: number
  time_ago: string
  content: string
  deleted?: boolean
  dead?: boolean
  type: string
  url?: string
  domain?: string
  comments: Article[] // Comments are items too
  level: number
  comments_count: number
}

export default Vue.extend({
  async asyncData({ params, res }) {
    const { id } = params
    const url = getApi(id)
    const resp = await axios.get(url)
    return { artile: resp.data }
  },

  data() {
    return {
      artile: {}
    }
  }
})
</script>