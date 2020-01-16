<template lang="html">
 <div>
   <h1>{{ beer.name }}</h1>
   <button type="button" v-if="!isFavourite" v-on:click="addFavouriteBeer">Add To Favourites</button>
   <dl>

     <dt></dt>
     <dd>{{beer.tagline}}</dd>

     <dt>Description</dt>
     <dd>{{beer.description}}</dd>

     <dt>ABV</dt>
     <dd>{{beer.abv}}</dd>

   </dl>
   <img v-bind:src="beer.image_url">
 </div>
</template>

<script>

import { eventBus } from '../main.js'

export default {
  name: 'beer-details',
  props: ['beer', 'isFavourite'],
  // data(){
  //   // isFavourite: null
  // },
  methods: {
    addFavouriteBeer(){
     eventBus.$emit('favourite-beer', this.beer.id)

    }
  }
}

</script>

<style lang="css" scoped>
</style>
