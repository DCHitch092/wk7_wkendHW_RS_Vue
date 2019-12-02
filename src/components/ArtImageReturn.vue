<template lang="html">
  <figure
  class="image-wrapper">
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
// import LazyLoad from './directives/LazyLoad.vue'
// change :src to :data-url="source.type"
// v-lazyload 

export default {
  name: "ArtImageReturn",
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
  // },
  // directives:   {
  //   lazyload: { inserted: el => {
  //     function loadImage() {
  //       const imageElement = Array.from(el.children)
  //       .find(el => el.nodeName === "IMG");
  //
  //       if (imageElement) {
  //         imageElement.addEventListener("load", () => {
  //           setTimeout(() => el.classList.add("loaded"), 100);
  //         });
  //
  //         imageElement.addEventListener("error", () => console.log("error"));
  //         imageElement.src = imag eElement.dataset.url;
  //
  //       }
  //     }
  //
  //     function handleIntersect(entries, observer) {
  //       entries.forEach(entry => {
  //         if (entry.isIntersecting) {
  //           loadImage();
  //           observer.unobserve(el);
  //         }
  //       });
  //     }
  //
  //     function createObserver() {
  //       const options = {
  //         root: null,
  //         threshold: "0"
  //       };
  //       const observer = new IntersectionObserver(handleIntersect, options);
  //       observer.observe(el);
  //     }
  //
  //     if (window["IntersectionObserver"]) {
  //       createObserver();
  //     } else {
  //       loadImage();
  //     }
  //
  //     }
  //   }
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
