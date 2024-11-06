<template>
    <div class="pokemon-card">
      <img
        :src="pokemonImage"
        :style="filterStyle"
        alt="Pokemon silhouette"
        class="pokemon-image"
      />
      <div v-if="!isDiscovered" class="guess-section">
        <input v-model="userInput" placeholder="¿Quién es este Pokémon?" />
        <button @click="checkAnswer">Descubrir</button>
      </div>
      <p v-else class="pokemon-name">{{ pokemonName }}</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    props: ['pokemonUrl'],
    data() {
      return {
        pokemonName: '',
        pokemonImage: '',
        userInput: '',
        isDiscovered: false,
      };
    },
    computed: {
      filterStyle() {
        return this.isDiscovered ? '' : 'filter: blur(5px) grayscale(100%);';
      },
    },
    mounted() {
      axios
        .get(this.pokemonUrl)
        .then(response => {
          this.pokemonName = response.data.name;
          this.pokemonImage = response.data.sprites.front_default;
        })
        .catch(error => console.log(error));
    },
    methods: {
      checkAnswer() {
        if (this.userInput.toLowerCase() === this.pokemonName) {
          this.isDiscovered = true;
          this.$emit('pokemonDiscovered');
        } else {
          alert('Nombre incorrecto. Inténtalo nuevamente.');
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .pokemon-card {
    text-align: center;
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 1rem;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    background-color: #f9fafb;
    transition: transform 0.2s ease;
  }
  
  .pokemon-card:hover {
    transform: scale(1.05);
  }
  
  .pokemon-image {
    width: 100px;
    height: 100px;
    margin-bottom: 0.5rem;
  }
  
  .guess-section {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  input {
    padding: 0.5rem;
    margin-bottom: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  button {
    padding: 0.5rem 1rem;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #45a049;
  }
  
  .pokemon-name {
    font-size: 1.25rem;
    font-weight: bold;
    color: #333;
  }
  </style>
  