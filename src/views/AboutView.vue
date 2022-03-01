<template>
  <div class="about">
    <h1>This is an about page</h1>
    <h3>{{ $route.params.slug }} </h3>
  </div>
</template>
<script>
import {useRoute} from "vue-router";
import {reactive, toRefs } from "vue";


export default {
  
  setup(){
      const route = useRoute();
      const state = reactive({
        pokemon:null
      })

      fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}` )
       .then((res) => res.json())
      .then((data) => {
        console.log(data);
        state.pokemon = data;
         
          })
          return{...toRefs(state)}
      
      
}}
</script>
