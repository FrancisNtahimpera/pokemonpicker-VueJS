<template>
  <div class="flex justify-center w-full">
    <input type="text" class="p-2 mt-10 border-2 border-blue-500" placeholder="enter poke name" 
      v-model="text"/>
  </div>
  <div class="flex flex-wrap justify-center p-4 mt-10">
    <div
      class="ml-4 text-blue-500 text-2x"
      v-for="(pokemon, idx) in filteredPokemon"
      :key="idx"
    >
    <router-link :to="`/about/${urlIdLookup[pokemon.name]}`" >{{ pokemon.name }}</router-link>
     </div>
  </div>
  
</template>

<script>
// @ is an alias to /src
import { computed, reactive, toRefs } from "vue";

export default {
   
  
  setup() {
    const state = reactive({
      pokemons: [],
      urlIdLookup: {}, 
      text:"",
      filteredPokemon: computed( ()=> updatePokemon() ),
    });
        fetch("https://pokeapi.co/api/v2/pokemon?offset=0")
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        state.pokemons = data.results;
        state.urlIdLookup = data.results.reduce((acc, cur, idx)=> 
           acc = {...acc, [cur.name]:idx+1 }
        ,{})
        console.log('url',state.urlIdLookup+1)
        
      });
    
    function updatePokemon(){
      if(!state.text){
        return []
      }
      
      return state.pokemons.filter((pokemon)=> pokemon.name.includes(state.text))
      
    }
    
 
      
    return { ...toRefs(state) };
  }
};
</script>
