<template>
    <div>
      <h1>Liste des bières IPA (Côté serveur)</h1>
      <ul>
        <li v-for="biere in bieres" :key="biere.id">{{ biere.name }}</li>
      </ul>
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  
  export default {
    setup() {
      const bieres = ref([]);
  
      const fetchBieres = async () => {
        try {
          const response = await fetch('https://api.sampleapis.com/beers/');
          const data = await response.json();
          bieres.value = data;
        } catch (error) {
          console.error(error);
        }
      };
  
      onMounted(fetchBieres);
      return {
        bieres,
      };
    },
  };
  </script>