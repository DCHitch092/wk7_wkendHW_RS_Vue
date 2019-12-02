<template lang="html">
<article id="selected-image">
  <h2>{{ theArtwork.artObject.longTitle }}</h2>
  <h3>{{ theArtwork.artObject.physicalMedium }}</h3>

  <img id="fullScreen" :src="theArtwork.artObject.webImage.url">
  <p>date:</p>
  <p>materials:</p>
  <a href="link">link</a>
  <p>return to view</p>
</article>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'artwork-detail',

  props: ['objectNumber'],

  data(){
    return{
      // selectedArt: {}
      theArtwork: ""
    }
  },

  methods: {
  // getInfo(){
  //
  //   }
  },

  computed: {
    selectedArt: function(){
      return fetch(`https://www.rijksmuseum.nl/api/en/collection/${this.objectNumber}?key=${process.env.VUE_APP_KEY}`)
        .then(response => response.json())
        .then(data => this.theArtwork = data)

    }
  },

  mounted(){
    eventBus.$on("image-clicked", selectionId => {
      this.objectNumber = selectionId;
    })
  }
}
</script>

<style lang="css" scoped>
h2{
  font-size: 3em;
}
#fullScreen{
  width: 100%;
}
</style>
