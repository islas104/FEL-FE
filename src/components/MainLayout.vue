<template>
    <div class="layout">
      <Header />
      <div class="content">
        <Sidebar />
        <MapView />
      </div>
    </div>
  </template>
  
  <script setup>
import Header from './Header.vue';
import MapView from './MapView.vue';
import Sidebar from './Sidebar.vue';
</script>
  
  <style scoped>
  .layout {
    display: flex;
    flex-direction: column;
    height: 100vh;
  }
  .content {
    display: flex;
    flex: 1;
  }
  </style>
  