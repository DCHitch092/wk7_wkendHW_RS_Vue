<template>
  <div id="app">

    <header>
      <nav>
        <img id="logo" src="/reijer-stolk-logo.svg" alt="logo for the reijer stolk vue app">
      </nav>

      <span id="tagline">a vue inside the artwork of  <b>Reijer Stolk</b>  (1896 - 1945)</span>

    </header>

    <section id="filters">
      <ul>
        <li>method1</li>
        <li>method2</li>
        <li>method3</li>
        <li>method4</li>
      </ul>
    </section>

    <section id="list-container">
      <art-list :artworks='artworks' />
    </section>

    <footer>

    </footer>
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
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
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
  justify-content: center;

}

#filters ul {
  display:flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
}

#filters ul li {
  margin: 0 0 1em 0;
}

#tagline {

}
section#list-container{
display: flex;
max-height: 15%;
max-width: 100%;
-ms-flex-wrap: wrap;
flex-wrap: wrap;
border: solid;
grid-row: 3 / 4;
grid-column: 1 / 1;
}

section#footer {
  grid-row: 3 / 4;
    grid-column: 1 / 1;
    background-color: #cc9966;
      color: #ffffcc;
}


</style>
