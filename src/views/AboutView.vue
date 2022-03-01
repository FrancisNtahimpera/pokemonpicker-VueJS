<template>
  <div class="about">
 
     <div v-if="pokemon"
          class="flex flex-col items-center justify-center w-3/12 m-auto mt-4 bg-purple-100 shadow-2xl"
     >
       <h3 class="text-2xl text-green-900 uppercase">{{ pokemon.name }}</h3>
         <div class="flex justify-center">
           <img class="w-200 " :src="pokemon.sprites.front_shiny" alt="">
            
         </div>
         <h3 class="text-yellow-400">Types</h3>
          <div v-for="(type,idx) in pokemon.types" :key="idx"   >
            <h5 class="text-blue-900">{{type.type.name }}</h5>
          </div>
          
      
     </div>
  </div>
</template>
<script>
import {useRoute} from "vue-router";
import {reactive, toRefs } from "vue";


export default {
  
  setup(){
      const route = useRoute();
      const pokemon = reactive({
        pokemon: null
      });

      fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/` )
       .then((res) => res.json())
      .then((data) => {
        pokemon.pokemon = data;
        console.log(data);
         
          });
          return{...toRefs(pokemon)}
      
      
}}
</script>
