<template lang="html">
  <div>
    <beer-select v-bind:beers="beers"></beer-select>
    <beer-details v-bind:beer="selectedBeer"></beer-details>
  </div>
</template>

<script>

import { eventBus } from './main.js'
import BeerSelect from './components/BeerSelect.vue'
import BeerDetails from './components/BeerDetails.vue'

export default {
  name: 'app',
  data(){
    return {
      beers: [],
      selectedBeerId: null,
      selectedBeer: null
    }
  },
  mounted(){
    fetch('https://api.punkapi.com/v2/beers')
    .then(result => result.json())
    .then(beers => this.beers = beers)

    eventBus.$on('beer-selected', (value) => {
      this.selectedBeerId = value
      this.findBeerById()
    })
  },
  components: {
    "beer-select": BeerSelect,
    "beer-details": BeerDetails
  },
  methods: {
    findBeerById() {
      return this.selectedBeer = this.beers.find(beer => beer.id === this.selectedBeerId)
    }
  }
}

</script>

<style lang="css" scoped>
</style>
