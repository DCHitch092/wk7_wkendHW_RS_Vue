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
        <li v-on:click="filterOne">method1</li>
        <li v-on:click="filterTwo">method2</li>
        <li v-on:click="filterThree">method3</li>
        <li v-on:click="filterFour">method4</li>
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
      // pressedOne: false;
      // pressedTwo: false;
      // pressedThree: false;
      // pressedFour: false;
    }
  },

  computed:{
    pressedClass: function() {
      return{
        // 'pressed': pressedClass;
      }
    }
  }
  ,


  methods: {
    filterOne(){
      // this.pressedClass = !this.pressedClass

    },
    filterTwo(){
      // this.pressedClass = !this.pressedClass
    },
    filterThree(){
      // this.pressedClass = !this.pressedClass
    },
    filterFour(){
      // this.pressedClass = !this.pressedClass
    },

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


</style>
