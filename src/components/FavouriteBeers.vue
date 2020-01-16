<template lang="html">

  <div>
    <h1>Favourite Beers:</h1>
    <div>
    <ul class="parent-flex">
      <li v-for="favouriteBeer of favouriteBeers" class="flex-center">
        <h2>{{ favouriteBeer.name }}</h2>
        <img v-bind:src="favouriteBeer.image_url">
      </li>
    </ul>
      </div>
  </div>

</template>

<script>
export default {
  name: 'favourite-beers',
  props: ['favouriteBeers']
}
</script>

<style lang="css" scoped>
div {
  background-color: indianred;
  padding: 0.5rem;
}

.parent-flex {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: nowrap;
  align-items: center;
}
.flex-center {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  text-align: center;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
