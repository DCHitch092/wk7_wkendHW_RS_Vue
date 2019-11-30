<template lang="html">
  <li class="artwork" :class="computedClass" v-if="artwork.hasImage">
    <!-- <art-list-return :imageObject="imageObject" /> -->
      <!-- {{ getOrientation() >= 1 ? true | false }} -->
      <!-- <img :src="artwork.webImage.url" /> -->
        <!-- {{ getOrientation() }}{{ checkCSS() }} -->
    <img class="jumble" :src="artwork.webImage.url" :alt="artwork.title"/>
  </li>
</template>

<script>
// import ArtImageReturn from './ArtImageReturn.vue'

export default {
  name: 'art-list-component',

  data() {
    return {
      // objectHeight: getHeight(),
      // objectWidth: getWidth(),
      // portaitSpan: "",
      // landscapeSpan: ""
      // orientation: "",
      // ratio: null
      // landscapeSpan: false,
      // portraitSpan: false
      // imageObject: this.artwork.webImage
    }
  },

  props: ['artwork'],

  computed: {
    objectWidth: function(){
      // return Math.round(this.artwork.webImage.width/400)
      return this.artwork.webImage.width
    },
    objectHeight: function(){
      // return Math.round(this.artwork.webImage.height/400)
      return this.artwork.webImage.height
    },
    orientation: function() {
        if (this.objectHeight > this.objectWidth) { return "portrait"}
        else if (this.objectHeight < this.objectWidth) { return "landscape"}
        else if (this.objectHeight === this.objectWidth) { return "square"};
      },
    ratio: function() {
      if (this.orientation === "portrait"){
        return this.objectHeight/this.objectWidth
      } else if (this.orientation === "landscape"){
        return this.objectWidth/this.objectHeight
      } else {return 1}
    },
    computedClass: function() {
      return {
            'square': this.ratio === 1,
            'landscapeExtraLong': this.ratio > 2 && this.ratio <= 3 && this.orientation === "landscape",
            'portraitExtraLong': this.ratio > 1.9 && this.ratio <= 3 && this.orientation === "portrait",
            'landscapeLong': this.ratio > 1.5 && this.ratio <= 2 && this.orientation === "landscape",
            'portraitLong': this.ratio > 1.5 && this.ratio <= 1.9 && this.orientation === "portrait",
            'landscapeMid': this.ratio > 1.2 && this.ratio <= 1.5 &&  this.orientation === "landscape",
            'portraitMid': this.ratio > 1.2 && this.ratio <= 1.5 && this.orientation === "portrait",
            'landscapeShort': this.ratio > 0 && this.ratio <= 1.2 && this.orientation === "landscape",
            'portraitShort': this.ratio > 0 && this.ratio <= 1.2 && this.orientation === "portrait",

        }}
},

  mounted() {
  },

  methods: {
    checkCSS: function() {
      if (this.orientation < 1) {
        this.landscapeSpan = true
      } else if (this.orientation > 1.4) {
        this.portraitSpan = true
      }
    },
    getCSS: function() {
      const portraitSpan = this.objectLength.round();
      const landscapeSpan = this.objectWidth.round();
      return `portrait-span-${portraitSpan} landscape-span-${landscapeSpan}`
    }
  },

  components: {
    // 'art-image-return': ArtImageReturn
  }
}
</script>

<style lang="css" scoped>
.square, .landscapeExtraLong, .landscapeLong, .landscapeMid, .landscapeShort, .portraitShort, .portraitMid, .portraitLong, .portraitExtraLong {
  display: flex; flex-direction: row; align-items: center; background-color: #ccc; flex-wrap: wrap;
}
/* .square{ grid-row-end: span 4; grid-column-end: span 4; }
.landscapeExtraLong{ grid-row-end: span 3; grid-column-end: span 4;  }
.landscapeLong{ grid-row-end: span 3; grid-column-end: span 4;}
.landscapeMid{ grid-row-end: span 3; grid-column-end: span 3;}
.landscapeShort{ grid-row-end: span 1; grid-column-end: span 2;}
.portraitExtraLong{ grid-row-end: span 6; grid-column-end: span 2; }
.portraitLong{ grid-row-end: span 8; grid-column-end: span 3; }
.portraitMid{ grid-row-end: span 6; grid-column-end: span 3;}
.portraitShort{ grid-row-end: span 4; grid-column-end: span 3;} */


.square{ grid-row-end: span 4; grid-column-end: span 3; }
.landscapeExtraLong{ grid-row-end: span 3; grid-column-end: span 3;  }
.landscapeLong{ grid-row-end: span 3; grid-column-end: span 3;}
.landscapeMid{ grid-row-end: span 3; grid-column-end: span 3;}
.landscapeShort{ grid-row-end: span 1; grid-column-end: span 3;}
.portraitExtraLong{ grid-row-end: span 9; grid-column-end: span 3; }
.portraitLong{ grid-row-end: span 8; grid-column-end: span 3; }
.portraitMid{ grid-row-end: span 6; grid-column-end: span 3;}
.portraitShort{ grid-row-end: span 5; grid-column-end: span 3;}


/* .square {
  grid-column-end: span 2;
  grid-row-end: span 2;

} */

img.jumble {
  max-width: 80%;
  margin: minmax(0.5em, 10%);
}
</style>
