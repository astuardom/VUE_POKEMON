<template>
  <div id="app">
    <img :src="pokemonLogo" alt="Logo de Pokémon" class="main-image" />
    <h1 class="title">¡Adivina el Pokémon!</h1>
    <PokeLista :discoveredCount="discoveredCount" @incrementCount="incrementCount" />
  </div>
</template>

<script>
import PokeLista from './components/PokeLista.vue';
// Importa la imagen del logo de Pokémon
import pokemonLogo from './assets/pokemon-23.svg';

export default {
  components: { PokeLista },
  data() {
    return {
      discoveredCount: 0,
      // Asigna la imagen importada a una propiedad de datos
      pokemonLogo
    };
  },
  methods: {
    incrementCount() {
      this.discoveredCount++;
    },
  },
};
</script>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
  background-color: #f3f4f6;
}

.title {
  color: #333;
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.main-image {
  width: 250px;
  margin-bottom: 1.5rem;
}
</style>
