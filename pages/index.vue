<template>
    <div>
        <h2>filtrer les bières</h2>
    <input type="number" v-model.number="priceMax" />
    <button @click="filterBieres">Filtrer</button>
    </div>
    <div>
      <h2 v-for="biere in bieres" :key="biere.id">
        <img :src="biere.image" />
        <NuxtLink :to="`/bieres-client/${biere.id}`">{{ biere.name }}</NuxtLink>
        <p>{{biere.price}}</p>
      </h2>
      
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref,computed, onMounted } from 'vue';
  import { useRoute,useRouter } from 'vue-router';
  
  const route = useRoute();
  const router = useRouter();

  const priceMax = ref<number>(route.query.pricemax ? parseFloat(route.query.pricemax as string) : 0);
  const bieres = ref<any>([]); 
  const beerType = ref(route.params.type);
  
  const fetchBieres = async () => {
    try {
      const response = await $fetch(`https://api.sampleapis.com/beers/${beerType}`);
      bieres.value = response;
    } catch (error) {
      console.error(error);
    }
}
  
  const bieresFiltered = computed(() => {
  return bieres.value.filter((biere:any) => biere.price <= priceMax.value);
});

const filterBieres = () => {
  const query = { pricemax: priceMax.value.toString() };
  router.push({ query });
};

onMounted(fetchBieres);
  </script>