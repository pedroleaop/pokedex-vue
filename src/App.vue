<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke,index) in pokemons" :key="index">
        <pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import pokemon from './components/pokemon.vue';
export default {
  components: { pokemon },
  name: 'App',
  data(){
    return {
        pokemons: []
    }
  },
 created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(response => (
      this.pokemons= response.data.results))
}}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
