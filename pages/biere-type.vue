<template>
    <div>
      <h1>{{ type }}</h1>
      <BiereList :biereType="type" />
    </div>
  </template>
  
  <script setup lang="ts">
  import { useRoute } from 'vue-router';
  import BiereList from '@/components/bieres-list.vue';
  
  const route = useRoute();
  const type = route.params.type;
  </script>