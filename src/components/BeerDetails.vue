<template lang="html">
  <div>
    <div class="parent-flex">
      <h1>{{ beer.name }}</h1>
      <button type="button" v-if="!isFavourite" v-on:click="addFavouriteBeer">Add To Favourites</button>
    </div>
    <dl class="parent-flex">

      <dt></dt>
      <dd>{{beer.tagline}}</dd>

      <dt>Description</dt>
      <dd>{{beer.description}}</dd>

      <dt>ABV</dt>
      <dd>{{beer.abv}}</dd>
      <img v-bind:src="beer.image_url">

    </dl>
  </div>
</template>

<script>

import { eventBus } from '../main.js'

export default {
  name: 'beer-details',
  props: ['beer', 'isFavourite'],
  methods: {
    addFavouriteBeer(){
      eventBus.$emit('favourite-beer', this.beer.id)

    }
  }
}

</script>

<style lang="css" scoped>
div {
  background-color: antiquewhite;

}
.parent-flex {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: nowrap;
  align-items: center;

}
</style>
