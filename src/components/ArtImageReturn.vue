<template lang="html">
  <figure class="image__wrapper">
      <img
        class="image__item"
        <!-- :src="source" -->
        alt="random image"
      >
    </figure>
</template>

<script>
export default {
  name: 'art-image-return',
  props: {
    source: {
      type: String,
      required: true
    }
  }
}

</script>

<style lang="css" scoped>
</style>
