<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <input class="input is-rounded" type="text" name="" id="" placeholder="Buscar Pokémon pelo nome" v-model="buscar"> 
    <div v-for="(poke,index) in resultadoBusca" :key="index">
      <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
     </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon'
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      buscar: ''
    }
  },
  components:{
    Pokemon
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=152&offset=0").then(res =>{
      this.pokemons = res.data.results;
    })
  },
  computed:{
    resultadoBusca: function() {
      if(this.buscar == '' || this.buscar == ' ') {
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.buscar)
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
</style>
