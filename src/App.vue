<template>
  <div id="app">

    <header>
      <nav>
        <img id="logo" src="/reijer-stolk-logo.svg" alt="logo for the reijer stolk vue app">
      </nav>

      <span id="tagline"><p>a vue inside the artwork of  <b>Reijer Stolk</b>  (1896 - 1945)</p></span>

    </header>

    <section :class="hiddenClass" class="selected-image">
      <artwork-detail :objectNumber="selectedImage" />
    </section>

    <section id="list-container">
      <art-list :artworks='artworks' />
    </section>

    <footer>

    </footer>


  </div>
</template>

<script>
import ArtList from './components/ArtList.vue'
import ArtworkDetail from './components/ArtworkDetail.vue'
import {eventBus} from "./main.js"
// import FilterButtons from './components/FilterButtons.vue'

export default {
  name: 'app',

  data() {
    return {
      artworks: [],
      facets: [],
      selectedImage: "",
      selectionHidden: true
    }
  },

  methods: {

    getEverything(){
      const promises = [1, 2, 3,4,5,6,7,8,9].map(num => {
      return fetch(`https://www.rijksmuseum.nl/api/en/collection?key=${process.env.VUE_APP_KEY}&involvedMaker=Reijer+Stolk&p=${num}&ps=12`)
        .then( response => response.json() )
      });

      Promise.all(promises)
      .then(data => {
        const artworksData = data
        .reduce((flat, toFlatten) => flat.concat(toFlatten.artObjects), [])
        .filter(item => item.hasImage === true)
              this.artworks = artworksData;
            }
          )

      // Promise.all(promises).then(data => {
      //   this.facets = data.facets[4];
      // })


    }
  },

  computed: {
    hiddenClass: function() {
      return {
        'hidden': this.selectionHidden === true
      }
    }
  },

  components: {
    "art-list": ArtList,
    "artworkDetail": ArtworkDetail
    // "filter-buttons": FilterButtons
  },

  mounted() {
    this.getEverything()

    eventBus.$on("image-clicked", selectionId => {
      this.selectedImage = selectionId;
      this.selectionHidden = !this.selectionHidden;
    })
    // this.getFacets()
  }
  //   fetch(`https://www.rijksmuseum.nl/api/en/collection?key=${ process.env.VUE_APP_KEY }&involvedMaker=Reijer+Stolk&ps=100`)
  //   .then(response => response.json())
  //   .then(data => this.artworks = data.artObjects)
  // }
}
</script>

<style>
#app  {
  display: grid;
  grid-template-rows: 1fr auto auto 1fr;
  grid-template-columns: auto;
  margin: 0;
  padding: 0;
}

header {
  grid-row: 1 / 2;
  grid-column: 1 / 1;
  background: #ffffff;
  display: flex;
  justify-content: flex-start;
  flex-direction: column;
}

#logo {
  width: 25%;
    padding: 2em 2em 1em 2em;
}

header span {
  background-color: #cc9966;
    color: #ffffcc;
    display: flex;
    justify-content: center;
    padding: 0.5em 0;
    font-size: 1.5em;
}

header span b {
  padding: 0 0.3em;
}

section#filters {
  grid-row: 2 / 3;
  grid-column: 1 / 1;
  display: flex;
  align-items: center;
  justify-content: space-evenly;

}

#filters ul {
  display:flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
  margin: 1em 0em;
}

#filters li {
  padding: 1em;
  background-color: #cc9966;
  margin: 0.4em;
}

.pressed{
  background-color: #993300;
  color: #cccccc;
}

#tagline {

}
section#list-container{
display: flex;
max-height: 15%;
max-width: 100%;
flex-wrap: wrap;
grid-row: 3 / 4;
grid-column: 1 / 1;
}

section#footer {
  grid-row: 3 / 4;
    grid-column: 1 / 1;
    background-color: #cc9966;
      color: #ffffcc;
}

.selected-image{
  background-color: rgba(255, 255, 255, 0.9);
    z-index: 1;
    display: block;
    position: fixed;
    padding: 6%;
    top: 25vh;
    margin-left: -18%;
    left: 25vw;
    color: #999999;
}

.hidden{
  visibility: hidden;

}

</style>
