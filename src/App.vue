<template>
  <div>
    <div class="column is-mobile">
      <img style="backgroung color: none;" src="./assets/pokelogo.webp" alt="Pokédex"> 
      <br><input type="text"  class="input is-danger" placeholder="Buscar Pokémon pelo nome" v-model="busca">
     <button id="buttonid" class="button is-fullwidth is-success" @click="buscar">Buscar</button>
 <p><button style="margin-top:1%;" class="button is-large">
    <span class="icon is-medium">
      <i class="fab fa-github"></i>
    </span>
    <a href="https://github.com/pedroleaop/" target="_blank"><span>GitHub</span></a>
  </button> 
  <button style="margin-top: 1%; margin-left:1%; background-color: #bbffbe;" class="button is-large">
    <span class="icon">
      <i class="fab fa-twitter"></i>
    </span>
    <a href="https://www.google.com/" target="_blank"><span>@pedroleaop</span></a></button>
  </p>
      <div v-for="(poke,index) in filteredPokemons" :key="index">
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
  computed: { /*
    resultadoBusca: function(){
      if(this.busca =='' || this.busca == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    } */
  },
  name: 'App',
  data(){
    return {
        pokemons: [],
        busca:'',
        filteredPokemons: []
    }
  },
 created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(response => (
      this.pokemons= response.data.results,
      this.filteredPokemons = response.data.results));
      
},
methods:{
  buscar: function(){
    this.filteredPokemons = this.pokemons;
    if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
    }else{
      this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
    }
  }
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
  margin-top: 60px;
}

body {
  background: #000 url('https://media.istockphoto.com/vectors/pixel-noise-of-analog-channel-grain-screen-seamless-background-vector-vector-id1023476960') repeat;
  }

  #buttonid {
    margin-top: 1%;
  }
</style>
