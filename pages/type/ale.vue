<template>
    <NuxtLink :to="`/type/${$route.params.type}`">{{ $route.params.type }}</NuxtLink>
    <div>
    <h2 v-for="biere in bieres" :key="biere.id">
      <img :src="biere.image" />
      <NuxtLink :to="`/bieres-client/${biere.id}`">{{ biere.name }}</NuxtLink>
      <p>{{biere.price}}</p>
    </h2>
    
  </div>
    
  </template>
  
  <script setup lang="ts">
  definePageMeta({
    path: '/type/:type',
    layout: 'custom'
  })

  import { ref,computed, onMounted } from 'vue';
  import { useRoute,useRouter } from 'vue-router';

  const route = useRoute();
const router = useRouter();

const priceMax = ref<number>(route.query.pricemax ? parseFloat(route.query.pricemax as string) : 10);
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

const bieresFiltered = computed(() => {
return bieres.value.filter((biere) => biere.price <= priceMax.value);
});

onMounted(fetchBieres);
  </script>



