<template lang="html">
  <div>
    <select v-model="selection">
      <option v-for="beer of beers" v-bind:value="beer.id" v-bind:key="beer.id">{{ beer.name }}</option>
    </select>
  </div>
</template>

<script>

export default {
  name: 'beer-select',
  props: ['beers'],
  data(){
    return {
      selection: null
    }
  }
}

</script>

<style lang="css" scoped>
</style>
