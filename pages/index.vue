<template>
  <div>
    <img :src="picture" />
    <h1>{{ status }}</h1>
    <button @click="onGetNewPicture">Get new picture</button>
    <button @click="onGoToAiredale">Go to dog airedale breed</button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

interface Response {
  message: string
  status: string
}

export default Vue.extend({
  async asyncData({ $axios }) {
    const data = await $axios.$get<Response>(
      'https://dog.ceo/api/breeds/image/random'
    )
    return { picture: data.message, status: data.status }
  },
  data() {
    return {
      picture: 'foo',
      status: 'loading'
    }
  },
  methods: {
    async onGetNewPicture() {
      this.status = 'loading'
      const data = await this.$axios.$get<Response>(
        'https://dog.ceo/api/breeds/image/random'
      )
      this.picture = data.message
      this.status = data.status
    },
    onGoToAiredale() {
      this.$router.push('/breed/airedale')
    }
  }
})
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
