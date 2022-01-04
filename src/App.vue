<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
    </div>
    <router-view/>
    <section class="pokelist">
      <h2> Pokemons présents : </h2>

      <Pokemons
          v-for="pokemon in info" :key="pokemon.id"
          :url = pokemon.url
      />

    </section>
  </div>
</template>
<script>

import Pokemons from "@/components/Pokemons"
import axios from "axios";

export default{
  name: "App",
  components:{
    Pokemons
  },
  data(){
    return {
      info: []
    }
  },
  mounted () {
    axios
        .get('https://pokeapi.co/api/v2/pokemon/?limit=20&offset=20')
        .then(response => (this.info = response.data.results))
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  align-content: center;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
