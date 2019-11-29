<template lang="html">
  <li v-if="artwork.hasImage">
    <!-- <art-list-return :imageObject="imageObject" /> -->
      <img :src="artwork.webImage.url" />
    <!-- <img src="/test.jpg" :alt="artwork.title"> --></li>
</template>

<script>
// import ArtImageReturn from './ArtImageReturn.vue'

export default {
  name: 'art-list-component',
  data() {
    return {
      // imageObject: this.artwork.webImage
    }
  },
  props: ['artwork'],
  components: {
    // 'art-image-return': ArtImageReturn
  }
}
</script>

<style lang="css" scoped>
li
{
  width: 25%;
  margin: 0 auto;
}
  img {
  width: 100%;
}
</style>
