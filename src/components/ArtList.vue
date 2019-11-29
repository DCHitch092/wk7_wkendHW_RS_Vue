<template lang="html">
  <ul id="artwork-container">
    <art-list-component v-for="(artwork, index) in artworks"  :artwork="artwork"/>
  </ul>
</template>

<script>
import ArtListComponent from './ArtListComponent.vue'

export default {
  name: 'art-list',
  props: ['artworks'],
  components: {
    "art-list-component": ArtListComponent
  }
}
</script>

<style lang="css" scoped>
ul{
  display: flex;
  flex-wrap: wrap;
}
</style>
