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
      // selectedBeerId: null,
      selectedBeer: null,
      favouriteBeers: []
    }
  },
  mounted(){
    fetch('https://api.punkapi.com/v2/beers')
    .then(result => result.json())
    .then(beers => this.beers = beers)

    eventBus.$on('beer-selected', (id) => {
      // this.selectedBeerId = value
      this.selectedBeer = this.findBeerById(id)
    })

    eventBus.$on('favourite-beer', (id) =>{
      this.favouriteBeers.push(this.findBeerById(id))
    })
  },
  components: {
    "beer-select": BeerSelect,
    "beer-details": BeerDetails
  },
  methods: {
    findBeerById(id) {
      return this.beers.find(beer => beer.id === id)
    }
  }
}

</script>

<style lang="css" scoped>
</style>
