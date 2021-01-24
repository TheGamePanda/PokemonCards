<template>
  <div>
    <!--  <div style="padding-top:146px;">-->
    <div id="card-deck">
      <compPokemon
        v-bind:title="pokemon.name.english"
        v-bind:health="pokemon.base.HP"
        v-bind:descr="pokemon.height"
        v-bind:type="pokemon.type"
        v-bind:image="pokemon.id"
        v-for="(pokemon, idx) in pokemon"
        :key="idx"
      >
      </compPokemon>
      <!-- Allows final card(s) to show correctly -->
      <span style="display:block;height:100px;"></span>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import compPokemon from "../components/card-component.vue";
const pokemonList = require("@/pokemon/pokedex.json");

export default {
  name: 'HelloWorld',
  components: {
    compPokemon
  },
  data(){
    return{
      red:"255",
      green:"000",
      blue:"000",
      fire:"fire",
      numberofPokemon: pokemonList.length
    }
  },
  methods:{
    getRandomInt(max) {
      return Math.floor(Math.random() * Math.floor(max));
    }

  },
  computed:{
    pokemon(){
      let pokemon = [...new Array(pokemonList.length)];
      for (let i = 0; i < pokemonList.length; i += 1) {
        pokemon.forEach((_, idx) => {
          if (idx == i) {
            pokemon[i] = pokemonList[idx];
          }
        });
      }
      return pokemon;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    #card-deck{
      overflow: scroll;
      overflow-x: hidden;
      /*height:calc(100vh - 177px);*/
      height:100vh;
      padding-top:29px;
      /* Hides scrollbar from page: */
      width:calc(100% + 17.5px);
      margin-right:17.5px;
      z-index:500;
    }
</style>