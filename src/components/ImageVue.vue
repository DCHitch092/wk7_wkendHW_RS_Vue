<template lang="html">
  <figure class="image-wrapper">
      <img
        class="jumble"
        :src="source.type"

        :alt="source.title"
        @mouseover="hoverStatus = true"
        @mouseout="hoverStatus = false"
      >
        <figcaption :class="onHoverClass">{{ source.title }}</figcaption>
    </figure>


</template>

<script>

export default {
  name: "ImageVue",

  computed:{
      onHoverClass: function() {
        return{
          'onHover': this.hoverStatus
        }
      }
  },

  data() {
    return{
      hoverStatus: false
    }
  },

  props: ["source"],
  
  methods: {
  }
}

</script>

<style lang="css" scoped>
.image-wrapper{
display: flex;
justify-content: center;
align-items: center;
flex-direction: column;
}

figcaption{
  padding: 0.5em 1em 0.5em 0.5em;
  background-color: rgba(204, 153, 102, 1);
  color: rgba(255,255,204,1);
  width: 50%;
  justify-content: center;
  display: flex;
  align-self: center;
  margin: -1em 0em 0em 0;
  flex-wrap: wrap;
  visibility: hidden;
}

.onHover{
  visibility: visible;
}

img.jumble {
  max-width: 80%;
  margin: minmax(0.5em, 10%);
}
</style>
