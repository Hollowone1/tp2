<script setup lang="ts">
import {onMounted, ref} from 'vue';
import {useRoute} from 'vue-router';

const biere = ref([]);
const route = useRoute()
const id = route.params.id;
const fetchBieres = async () => {
  try {
    const response = await fetch(`https://api.sampleapis.com/beers/ale/${id}`);
    biere.value = await response.json();
  } catch (error) {
    console.error(error);
  }
};

onMounted(fetchBieres);
</script>

<template>
<!--  { "price": "$16.99", "name": "Founders All Day IPA", "rating": { "average": 4.411243509154233, "reviews": 453 }, "image": "https://www.totalwine.com/media/sys_master/twmmedia/h00/h94/11891416367134.png", "id": 1 }-->
  <div v-if="biere">
    <h1>Details de la bière</h1>
    <h2>{{ biere.name }}</h2>
    <img :src="biere.image" alt="Pas d'images" />
    <p>{{ biere.price }}</p>


  </div>
</template>

<style scoped>

</style>