<template lang="html">
  <ul id="artwork-container">
    <art-list-component v-for="(artwork, index) in artworks"
    :artwork="artwork"
    />
    <!-- <art-list-fetch v-for="(artwork, index) in artworks"
    :objectID="artwork.objectNumber"
    /> -->
  </ul>
</template>

<script>
// :artwork="artwork"
// import ArtListFetch from './ArtListFetch.vue'
import ArtListComponent from './ArtListComponent.vue'

export default {
  name: 'art-list',
  props: ['artworks'],
  components: {
    "art-list-component": ArtListComponent
    // "art-list-fetch": ArtListFetch

  }
}
</script>

<style lang="css" scoped>

ul#artwork-container{
    display: grid;
    grid-template-columns: repeat(12, minmax(2em, 0.5fr));
    grid-gap: 0.4em;
    /* grid-auto-flow: row dense; */
    list-style: none;
    grid-auto-rows: 5em;
}

li.artwork {
    justify-content: center;
    align-items: center;
}

li.artwork img {
  max-width: 90%
}

</style>
