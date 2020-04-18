<template>
  <div>
    <img :src="picture" />
    <button @click="onGoBack">Go back</button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

interface Response {
  message: string
  status: string
}

export default Vue.extend({
  async asyncData({ $axios, params }) {
    const data = await $axios.$get<Response>(
      `https://dog.ceo/api/breed/${params.id}/images/random`
    )
    return { picture: data.message }
  },
  data() {
    return {
      picture: ''
    }
  },
  methods: {
    onGoBack() {
      this.$router.push('/')
    }
  }
})
</script>
