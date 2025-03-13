<template>
    <aside class="sidebar">
      <h2>Farmers</h2>
      <ul>
        <li v-for="farmer in farmers" :key="farmer.id">{{ farmer.name }}</li>
      </ul>
    </aside>
  </template>
  
  <script setup>
import { ref } from 'vue';

const farmers = ref([
    { id: 1, name: "John Doe" },
    { id: 2, name: "Jane Smith" },
    { id: 3, name: "Mark Johnson" },
  ]);
  
</script>
  
  <style scoped>
  .sidebar {
    width: 250px;
    background-color: #34495e;
    color: white;
    padding: 1rem;
    height: 100vh;
  }
  </style>
  