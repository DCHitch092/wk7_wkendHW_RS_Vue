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
  name: "filterButtons",

  props: ['facets'],

  date() {
    return {
    }
  },
  // props: ['artworks'],
  computed: {
  }
}

</script>

<style lang="css" scoped>
</style>
