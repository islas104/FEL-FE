<script setup>
import 'leaflet/dist/leaflet.css';

import {
    defineProps,
    onMounted,
    watch,
} from 'vue';

import L from 'leaflet';

// Props from MainLayout
const props = defineProps({
  role: String,
  fields: Array,
  center: Array,
});

let map;

// Initialize map
onMounted(() => {
  map = L.map('map').setView(props.center, 13);

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);

  renderPolygons();
});

// Function to render polygons dynamically
const renderPolygons = () => {
  map.eachLayer((layer) => {
    if (layer instanceof L.Polygon) map.removeLayer(layer);
  });

  props.fields.forEach((field) => {
    const polygon = L.polygon(field.boundary, {
      color: props.role === 'Unlock Team' || props.role === 'PU Manager' || props.role === 'FF' ? 'blue' : 'gray',
      fillOpacity: 0.5,
    }).addTo(map);

    if (props.role === 'Unlock Team' || props.role === 'PU Manager' || props.role === 'FF') {
      polygon.on('click', () => alert(`Editing Field ID: ${field.id}`));
    }
  });
};

// Watch role changes & update map dynamically
watch(() => props.role, () => {
  renderPolygons();
});
</script>

<template>
  <div>
    <div id="map"></div>
    <p v-if="['Unlock Team', 'PU Manager', 'FF'].includes(role)">You can edit the fields.</p>
    <p v-else>You have view-only access.</p>
  </div>
</template>

<style scoped>
#map {
  width: 100%;
  height: 100vh;
}
</style>
