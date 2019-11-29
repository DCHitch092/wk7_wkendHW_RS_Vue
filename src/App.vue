<template>
  <div id="app">
    <header>
      <nav>
        <img id="logo" src="/reijer-stolk-logo.svg" alt="logo for the reijer stolk vue app">
        <ul>
          <li></li>
        </ul>
      </nav>
      <span id="tagline">a vue inside the artwork of Reijer Stolk (1896 - 1945)</span>
    </header>
    <ul>
      <li>method1</li>
      <li>method2</li>
      <li>method3</li>
      <li>method4</li>
    </ul>
    <art-list :artworks='artworks' />

  </div>
</template>

<script>
import ArtList from './components/ArtList.vue';

export default {
  name: 'app',

  data() {
    return {
      artworks: [],
    }
  },

  components: {
    "art-list": ArtList,
  },

  mounted() {
    fetch(`https://www.rijksmuseum.nl/api/nl/collection?key=${ process.env.VUE_APP_KEY }&involvedMaker=Reijer+Stolk&ps=100`)
    .then(response => response.json())
    .then(data => this.artworks = data.artObjects)
  }
}
</script>

<style>
#app  {
  display: grid;
  grid-template-rows: 200px 1fr 6fr 2fr 1fr;
  grid-template-columns: auto;
    width: 95%;
    border: 1px solid #000;
}

header {
  grid-row: 0 1;
  grid-column: 0 1;
  border: 1px solid #000;
}

header span {

  background-color: ;
}

#logo {
  width: 25%;
}
</style>
