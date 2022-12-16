<template>
  <div class="list">
    <article v-for="pokemon in pokemonsFiltered" v-bind:key="pokemon.order" v-on:click="ShowDetail(pokemon)">
      <h3>{{ pokemon.name }}</h3>
      <img v-bind:src="IMG_URL+pokemon.name+'.png'" />
    </article>
  </div>
</template>

<script>
import axios from 'axios'
const _ = require("lodash");
export default{
  mounted() {
    axios
      .get('https://pokeapi.co/api/v2/pokemon')
      .then(response =>  (this.liste_pokemon = response.data.results))
  },
  data : function(){
    return {
      
      liste_pokemon : [],
      IMG_URL : "https://img.pokemondb.net/sprites/bank/normal/"
      }
    },
    props : ["result_search"],

    methods: {
      ShowDetail: function(pokemon){
        this.$emit("ShowDetail",pokemon)
      },
    },

    computed: {
      pokemonsFiltered: function(){ 
        if (this.result_search == ""){
          return this.liste_pokemon
      }

      else{
        return _.filter(this.liste_pokemon, v => v.name.includes(this.result_search))
       }
    }
  },
 };
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>

