<script setup>
import 'leaflet/dist/leaflet.css';

import {
    onMounted,
    ref,
} from 'vue';

import L from 'leaflet';  // Import Leaflet directly

// Default center point (latitude, longitude)
const center = ref([51.505, -0.09]);

// Placeholder field boundaries (Replace with API data)
const fields = ref([
  { id: 1, boundary: [[51.505, -0.09], [51.51, -0.1], [51.52, -0.08]] },
  { id: 2, boundary: [[51.49, -0.1], [51.50, -0.12], [51.48, -0.08]] },
]);

onMounted(() => {
  const map = L.map("map").setView(center.value, 13);

  // Add tile layer
  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png").addTo(map);

  // Add polygons for field boundaries
  fields.value.forEach((field) => {
    L.polygon(field.boundary).addTo(map);
  });
});
</script>

<template>
  <div id="map" style="height: 100vh; width: 100%;"></div>
</template>

<style scoped>
#map {
  width: 100%;
  height: 100vh;
}
</style>
