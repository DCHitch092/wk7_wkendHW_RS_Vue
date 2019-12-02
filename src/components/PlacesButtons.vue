<template lang="html">
  <ul >
    <li v-for="place in places" v-on:click="">{{ place }}</li>
    <!-- <li v-on:click="filterOne">method1</li>
    <li v-on:click="filterTwo">method2</li>
    <li v-on:click="filterThree">method3</li>
    <li v-on:click="filterFour">method4</li> -->
  </ul>
</template>

<script>
export default {
  name: "placesButtons",
  date() {
    return {
      places: ["Netherlands", "Paris", "The Hague"]
    }
  },
  // props: ['artworks'],
  computed: {
      placesList: function() {
        const placesArray = [];
        this.artworks.forEach(artwork => {
          const placeName = artwork.productionPlaces[0];
          if (placesArray.indexOf(placeName) !== NaN) {
            placesArray.push(placeName);
          }
        })
        return placesArray;
      }}
}

</script>

<style lang="css" scoped>
</style>
