<template lang="html">
  <div>
    <beer-select v-bind:beers="beers"></beer-select>
  </div>
</template>

<script>


import BeerSelect from './components/BeerSelect.vue'

export default {
  name: 'app',
  data(){
    return {
      beers: []
    }
  },
  mounted(){
    fetch('https://api.punkapi.com/v2/beers')
    .then(result => result.json())
    .then(beers => this.beers = beers)
  },
  components: {
    "beer-select": BeerSelect
  }
}

</script>

<style lang="css" scoped>
</style>
