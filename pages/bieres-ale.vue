<template>
    <NuxtLink :to="`/type/${$route.params.type}`">{{ $route.params.type }}</NuxtLink>
  </template>
  
  <script setup lang="ts">
  definePageMeta({
    path: '/type/:type',
    layout: 'custom'
  })
  </script>