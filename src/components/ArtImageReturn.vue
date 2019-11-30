<template lang="html">
  <figure v-lazyload class="image-wrapper">
      <img
        class="jumble"
        :data-url="source.type"
        alt="random image"
      >
    </figure>


</template>

<script>
// import LazyLoad from './directives/LazyLoad.vue'

export default {
  name: "ArtImageReturn",
  props: ["source"],
  directives:   {
    lazyload: { inserted: el => {
      function loadImage() {
        const imageElement = Array.from(el.children)
        .find(el => el.nodeName === "IMG");

        if (imageElement) {
          imageElement.addEventListener("load", () => {
            setTimeout(() => el.classList.add("loaded"), 100);
          });

          imageElement.addEventListener("error", () => console.log("error"));
          imageElement.src = imageElement.dataset.url;

        }
      }

      function handleIntersect(entries, observer) {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            loadImage();
            observer.unobserve(el);
          }
        });
      }

      function createObserver() {
        const options = {
          root: null,
          threshold: "0.25"
        };
        const observer = new IntersectionObserver(handleIntersect, options);
        observer.observe(el);
      }

      if (window["IntersectionObserver"]) {
        createObserver();
      } else {
        loadImage();
      }

    }
  }}
}

</script>

<style lang="css" scoped>
.image-wrapper{
display: flex;
justify-content: center;
align-items: center;
}

img.jumble {
  max-width: 80%;
  margin: minmax(0.5em, 10%);
}
</style>
