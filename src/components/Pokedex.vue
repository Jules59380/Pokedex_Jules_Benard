<template>
  <div class="container">
    <PokemonSearch @search="setPokemonSearch" />
    <PokemonDetail :pokemonUrl="pokemonUrl" :pokeimg="pokeImg" v-if="visible==true" v-on:closeDetail='Hide'/>
    <PokemonList v-on:ShowDetail='Show' :result_search="result_search"/>
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";

export default {
  data : function(){
    return {
      visible : false,
      pokemon : [],
      pokemonUrl : '',
      pokeImg : '',
      result_search : '',
      }
    },
  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
  },
  methods: {
      Hide:function(){
        this.visible = false
      },
      Show:function(pokemon){
        console.log(pokemon)
        this.visible = true
        this.pokemon = pokemon
        this.pokemonUrl = pokemon.url
        this.pokemonImg = pokemon.img  
      },
      setPokemonSearch( searchBarContent ) {
        this.result_search = searchBarContent;
      }
  }
}
      
;
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>