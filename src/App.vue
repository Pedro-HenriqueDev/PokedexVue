<template>
  <div id="app">
    <div class="head">
      <div>
        <a href="/">
          <img class="pokemon-word" src="./assets/pokemon.png" alt="">
        </a>
      </div>
      <div class="search">
        <div>
            <input class="input input-search" type="text" placeholder="Pesquisar" v-model="search">
        </div>
        <div>
          <form>
            <div @click="searchPokemon">
                <img class="pokebola" src="./assets/pokeball.png" alt="">
            </div>
          </form>
        </div>
          
      </div>
      
    </div>
    <div class="conteudo">
      <div class="container-pok">
        <ul v-for="(poke,index) in filteredPokemons" :key="poke.url">
            <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
        </ul>
      </div>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      search: ''
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=150&offset=0").then(res => {
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    }).catch(err => {
      console.log(err);
      alert("Ocorreu um erro")
    })
  },
  components: {
    Pokemon
  },
  methods: {
    searchPokemon() {
        this.filteredPokemons = this.pokemons
      if(this.search == '' || this.search == ' ') {
        this.filteredPokemons = this.pokemons
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.search.toLowerCase())
      }
    }
  }
}
</script>

<style >
.conteudo {
  display: flex;
  justify-content: center;
}
.container-pok {
  width: 90%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.head {
  display: flex;
  justify-content: space-between;
  background: rgb(255, 196, 32);
  box-shadow: 0px 0px 5px 1px rgba(0, 0, 0, 0.5);
  margin-bottom: 40px;
  height: 80px;
}
.pokemon-word {
  margin: 10px;
  width: 150px;
}
.pokebola {
  width: 45px;
  margin-left: 10px;
  cursor: pointer;
}
.search {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
    margin-right: 20px;
}
@media (max-width: 576px){
.pokemon-word {
  margin: 10px;
  width: 90px;
}
.pokebola {
  width: 35px;
}
}
</style>
