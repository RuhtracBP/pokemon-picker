<template>
  <div class="about">
    <div v-if="pokemon" class="w-3/12 p-6 m-auto bg-purple-100 shadow-2xl rounded flex justify-center flex-col items-center">
      <h3 class="text-2xl text-green-900 uppercase">{{pokemon.name}}</h3>
      <div class="flex justify-center">
        <img class="w-48" :src="pokemon.sprites.front_default" alt="">
        <img class="w-48" :src="pokemon.sprites.back_default" alt="">
      </div>
      <h3 class="text-yellow-400">Types</h3>
      <div v-for="(type, idx) in pokemon.types" :key="idx">
        <h5 class="text-blue-900 font-bold">{{type.type.name}}</h5>
      </div>
    </div>
  </div>
</template>

<script>
import { useRoute } from 'vue-router';
import { reactive, toRefs } from 'vue';

export default {
  setup() {
    const route = useRoute();

    const state = reactive({
      pokemon: null
    })

    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}`)
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        state.pokemon = data;
      })

      return {...toRefs(state)}
  },
}
</script>