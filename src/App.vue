<template lang="html">
  <div>
    <div class="selection-wrapper">
      <h1>Choose a beer:</h1>
      <beer-select v-bind:beers="beers"></beer-select>
      <button v-on:click="toggleFavourite">Favourite Beers</button>
    </div>


    <favourite-beers v-if="favouriteBeers && showFavourites" v-bind:favouriteBeers="favouriteBeers"></favourite-beers>

    <beer-details v-if="selectedBeer" v-bind:isFavourite="isAlreadyFavourite(selectedBeer.id)"  v-bind:beer="selectedBeer" ></beer-details>

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
      favouriteBeers: [],
      showFavourites: false
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
      if (!this.isAlreadyFavourite(id)) {
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
      return this.favouriteBeers.map(beer => beer.id).includes(id)
  },
    toggleFavourite() {
      this.showFavourites = !this.showFavourites

    }
}
}
</script>

<style lang="css">
img {
  height: 12rem;
  margin: 1rem;
}


button {
  margin: 1rem;
}

.selection-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

</style>
