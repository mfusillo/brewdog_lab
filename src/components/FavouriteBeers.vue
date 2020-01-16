<template lang="html">

  <div>
    <ul>
      <li v-for="favouriteBeer of favouriteBeers">
        <h2>{{ favouriteBeer.name }}</h2>
        <img v-bind:src="favouriteBeer.image_url">
      </li>
    </ul>
  </div>

</template>

<script>
export default {
  name: 'favourite-beers',
  props: ['favouriteBeers']
}
</script>

<style lang="css" scoped>
</style>
