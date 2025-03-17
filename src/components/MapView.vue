<script setup>
import 'leaflet/dist/leaflet.css';

import {
    defineProps,
    onMounted,
    watch,
} from 'vue';

import L from 'leaflet';

const props = defineProps({
  role: {
    type: String,
    required: true
  },
  fields: {
    type: Array,
    required: true
  },
  center: {
    type: Array,
    required: true
  }
});

let map = null;

onMounted(() => {
  // Initialize the map with basic options
  map = L.map('map', { zoomControl: false }).setView(props.center, 13);

  // Add OpenStreetMap tile layer with attribution
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; OpenStreetMap contributors'
  }).addTo(map);

  renderPolygons();
});

// Render polygons based on fields data
const renderPolygons = () => {
  // Remove any previously rendered polygons
  map.eachLayer((layer) => {
    if (layer instanceof L.Polygon) {
      map.removeLayer(layer);
    }
  });

  // Define roles that have editing privileges
  const editableRoles = ['Unlock Team', 'PU Manager', 'FF'];

  // Render polygons for each field
  props.fields.forEach((field) => {
    const isEditable = editableRoles.includes(props.role);
    const polygon = L.polygon(field.boundary, {
      color: isEditable ? 'blue' : 'gray',
      fillOpacity: 0.5
    }).addTo(map);

    if (isEditable) {
      polygon.on('click', () => {
        alert(`Editing Field ID: ${field.id}`);
      });
    }
  });
};

// Re-render polygons when the role changes
watch(() => props.role, () => {
  renderPolygons();
});
</script>

<template>
  <div class="map-container">
    <div id="map"></div>
    <p class="access-message">
      <span v-if="['Unlock Team', 'PU Manager', 'FF'].includes(role)">
        You can edit the fields.
      </span>
      <span v-else>
        You have view-only access.
      </span>
    </p>
  </div>
</template>

<style scoped>
.map-container {
  position: relative;
}
#map {
  width: 100%;
  height: 100vh;
}
.access-message {
  position: absolute;
  bottom: 10px;
  left: 10px;
  background: rgba(255, 255, 255, 0.8);
  padding: 8px;
  border-radius: 4px;
  font-size: 0.9rem;
}
</style>
