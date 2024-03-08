<template>
    <div>
      <h2 v-for="biere in bieres" :key="biere.id">
        <img :src="biere.image" />
        <NuxtLink :to="`/bieres-client/${biere.id}`">{{ biere.name }}</NuxtLink>
      </h2>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  
  const route = useRoute();
  console.log(route.params.id);
  
  const bieres = ref<any[]>([]);
  
  const fetchBieres = async () => {
    try {
      const response = await fetch('https://api.sampleapis.com/beers/ale');
      const data = await response.json();
      bieres.value = data;
    } catch (error) {
      console.error(error);
    }
  };
  
  onMounted(fetchBieres);
  </script>