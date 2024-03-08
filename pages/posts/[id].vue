<script setup lang="ts">
const route = useRoute()
console.log(route.params.id)
</script>

<template>
    <h2 v-for="biere in bieres" :key="biere.id"><img :src="biere.image"><NuxtLink to="/bieres-client/1">{{ biere.name }}</NuxtLink></h2>
    
</template>

<script>
  import { ref, onMounted } from 'vue';
  
  export default {
    setup() {
      const bieres = ref([]);
  
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
      return {
        bieres,
      };
    },
  };
  </script>