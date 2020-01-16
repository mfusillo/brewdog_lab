<template lang="html">
  <div>
    <beer-select v-bind:beers="beers"></beer-select>
    <beer-details v-if="selectedBeer" v-bind:beer="selectedBeer"></beer-details>
    <favourite-beers v-if="favouriteBeers" v-bind:favouriteBeers="favouriteBeers"></favourite-beers>
  </div>
</template>

<script>

import { eventBus } from './main.js'
import BeerSelect from './components/BeerSelect.vue'
import BeerDetails from './components/BeerDetails.vue'
import FavouriteBeers from './components/FavouriteBeers.vue'

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
      if(!this.isAlreadyFavourite(id)){
      this.favouriteBeers.push(this.findBeerById(id))
      }
    })
  },
  components: {
    "beer-select": BeerSelect,
    "beer-details": BeerDetails,
    "favourite-beers": FavouriteBeers
  },
  methods: {
    findBeerById(id) {
      return this.beers.find(beer => beer.id === id)
    },
    isAlreadyFavourite(id) {
      return this.favouriteBeers.find(beer => beer.id === id)
    }
  }
}

</script>

<style lang="css" scoped>
</style>
