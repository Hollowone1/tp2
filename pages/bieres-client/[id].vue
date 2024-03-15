<script setup>
import {onMounted, ref} from 'vue';
import {useRoute} from 'vue-router';

const biere = ref([]);
const route = useRoute()
const id = route.params.id;
const fetchBieres = async () => {
  try {
      biere.value = await $fetch(`https://api.sampleapis.com/beers/ale/${id}`)
  } catch (error) {
    console.error(error);
  }
};

onMounted(fetchBieres);

</script>

<template>
  <div v-if="biere">
    <h1>Details de la bière</h1>
    <h2>{{ biere.name }}</h2>
    <img :src="biere.image" alt="Pas d'images" />
    <p>{{ biere.price }}</p>
  </div>
</template>

<style scoped>

</style>