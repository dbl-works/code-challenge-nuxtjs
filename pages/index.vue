<template>
  <Layout>
    <h1 class="text-2xl">
      DBL Code Challenge: Airports
    </h1>

    <h2 class="mt-10 text-xl">
      All Airports
    </h2>

    <div>
      <a v-for="airport in airports" :key="airport.iata" :href="`/airports/${airport.iata.toLowerCase()}`" class="mt-5 flex items-center shadow p-5 border">
        <div>
          {{ airport.name }}, {{ airport.city }}
        </div>
        <div class="ml-auto text-mono">
          {{ airport.country }}
        </div>
      </a>
    </div>
  </Layout>
</template>

<script lang="ts">
import Vue from 'vue'

import axios from '~/utils/axios'
import Layout from '~/components/Layout.vue'
import Airport from '~/types/airport'

interface Data {
  airports: Airport[]
}

export default Vue.extend({
  components: {
    Layout
  },
  data (): Data {
    return {
      airports: []
    }
  },
  mounted () {
    this.loadAirports()
  },
  methods: {
    async loadAirports () {
      const response = await axios.get<Airport[]>('/api/airports').catch(err => err.response)
      this.airports = response.data
    }
  }
})
</script>
