<template>
  <div id="app">
    <div v-for="(poke,index) in pokemons" :key="index">
      <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
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
      pokemons: []
    }
  },
  components:{
    Pokemon
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=152&offset=0").then(res =>{
      this.pokemons = res.data.results;
    })
    
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
