<template lang="html">
  <div>
    <select v-model="selection">
      <option v-for="beer of beers" v-bind:value="beer.id" v-bind:key="beer.id">{{ beer.name }}</option>
    </select>
  </div>
</template>

<script>

import { eventBus } from '../main.js'
export default {
  name: 'beer-select',
  props: ['beers'],
  data(){
    return {
      selection: null
    }
  },
  watch: {
    selection(value) {
      eventBus.$emit('beer-selected', value)
    }
  }

}

</script>

<style lang="css" scoped>
</style>
