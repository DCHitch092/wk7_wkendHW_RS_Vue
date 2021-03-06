<template lang="html">
  <li class="artwork" v-on:click="imageClick" :class="computedClass" v-if="artwork.hasImage">
    <section class="frame frame-top"><img src="cornerTop.svg" class="frame-element topRight" alt=""></section>
    <artImageReturn  :source="source" />
    <section class="frame frame-bottom"><img src="cornerBottom.svg" class="frame-element bottomLeft" alt=""></section>
  </li>
</template>

<script>
import ArtImageReturn from './ArtImageReturn.vue'
import { eventBus} from '../main.js'

export default {
  name: 'art-list-component',

  data() {
    return {
      imageObject: this.artwork.webImage,
      source: {
        type: this.artwork.webImage.url,
        title: this.artwork.title,
        required: true,
        place: this.artwork.productionPlaces[0]
      }
    }
  },

  props: ['artwork'],
  components: {
    'artImageReturn': ArtImageReturn
  },

  computed: {
    objectWidth: function(){
      return this.artwork.webImage.width
    },
    objectHeight: function(){
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
    imageClick(){
      eventBus.$emit("image-clicked", this.artwork.objectNumber);
    }
  }
}
</script>

<style lang="css" scoped>

.landscapeExtraLong, .landscapeMid, .landscapeLong, .square, .landscapeShort, .portraitExtraLong, .portraitLong, .portraitMid, .portraitShort {
  display: flex;
  flex-direction: row;
  align-items: center;
  flex-wrap: wrap;
  grid-column-end: span 3;
  /* background-color: rgba(255,255, 255, 0.6); */
}

.landscapeExtraLong, .landscapeMid, .landscapeLong {
  grid-row-end: span 3;
  /* background-color: rgba(255,255, 255, 0.7);  */
}

.square{ grid-row-end: span 4;}
.landscapeShort{ grid-row-end: span 4; }
.portraitExtraLong{ grid-row-end: span 9;}
.portraitLong{ grid-row-end: span 8; }
.portraitMid{ grid-row-end: span 6; }
.portraitShort{ grid-row-end: span 5;}

li{
  display: flex;
  flex-direction: column;
}

.frame {
  opacity: 0.2;
  width: 92%;
  display: flex;
  flex-direction: row;
}

.frame-top  {
  justify-content: flex-end;
   }

  .frame-bottom {
    justify-content: flex-start;
  }

.landscapeShort .frame-bottom, .landscapeMid .frame-bottom, .landscapeLong .frame-bottom, .landscapeExtraLong .frame-bottom {
  margin: -15% 4% 0em 0em;
}

.portraitShort .frame-bottom, .portraitMid .frame-bottom, .portraitLong .frame-bottom, .portraitExtraLong .frame-bottom {
    margin: -21% 4% 0em 0em;
  }

.landscapeShort .frame-top, .landscapeMid .frame-top, .landscapeLong .frame-top, .landscapeExtraLong .frame-top {
  margin-bottom: -2em;
  margin-top: 1em;
}

.portraitShort .frame-top, .portraitMid .frame-top, .portraitLong .frame-top, .portraitExtraLong .frame-top {
  margin-bottom: -2em;
  margin-top: 1em;
}

.frame-element { width:2em;}
/* .topRight { align-self: flex-end;}
.bottomLeft { align-self: flex-start;} */

</style>
