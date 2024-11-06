<template>
    <div>
      <h2 class="subtitle">Pokémones descubiertos: {{ discoveredCount }}/20</h2>
      <div class="pokemon-grid">
        <PokeCard
          v-for="(pokemon, index) in pokemons"
          :key="index"
          :pokemonUrl="pokemon.url"
          @pokemonDiscovered="incrementDiscoveredCount"
        />
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import PokeCard from './PokeCard.vue';
  
  export default {
    components: { PokeCard },
    props: ['discoveredCount'],
    data() {
      return {
        pokemons: [],
      };
    },
    mounted() {
      axios
        .get('https://pokeapi.co/api/v2/pokemon?limit=20')
        .then(response => {
          this.pokemons = response.data.results;
        })
        .catch(error => console.log(error));
    },
    methods: {
      incrementDiscoveredCount() {
        this.$emit('incrementCount');
      },
    },
  };
  </script>
  
  <style scoped>
  .subtitle {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    text-align: center;
  }
  
  .pokemon-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr); /* Cuatro columnas */
    gap: 1.5rem;
    padding: 1rem;
  }
  
  /* Ajuste de columnas para pantallas pequeñas */
  @media (max-width: 1024px) {
    .pokemon-grid {
      grid-template-columns: repeat(3, 1fr); /* Tres columnas */
    }
  }
  
  @media (max-width: 768px) {
    .pokemon-grid {
      grid-template-columns: repeat(2, 1fr); /* Dos columnas */
    }
  }
  
  @media (max-width: 480px) {
    .pokemon-grid {
      grid-template-columns: 1fr; /* Una columna */
    }
  }
  </style>
  