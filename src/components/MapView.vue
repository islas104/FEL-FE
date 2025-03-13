<script setup>
import 'leaflet/dist/leaflet.css';

import {
    onMounted,
    ref,
} from 'vue';

import L from 'leaflet';

// Props passed from the parent component (MainLayout)
const props = defineProps({
  role: String, // role passed from MainLayout
  fields: Array, // dynamic data passed as fields
  center: Array, // center of the map (latitude, longitude)
});

// Reactive map center point and fields (for dynamic behavior)
const mapCenter = ref(props.center || [51.505, -0.09]);  // Default center if not passed
const fields = ref(props.fields || []);  // Fields are dynamic

// Create a ref for the map instance
let map = null;

// Handle dynamic map rendering based on the role
onMounted(() => {
  map = L.map('map').setView(mapCenter.value, 13);

  // Add tile layer
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);

  // Dynamically add polygons or other features to the map based on fields
  fields.value.forEach((field) => {
    const polygon = L.polygon(field.boundary, {
      color: role === 'Unlock Team' ? 'blue' : 'gray', // Blue for editable, gray for view-only
      fillOpacity: 0.3,
    }).addTo(map);

    // If the role is Unlock Team, enable editing features
    if (role === 'Unlock Team') {
      polygon.on('click', (e) => {
        alert(`You clicked on field with ID: ${field.id}`);
        // Add additional functionality to allow editing, etc.
      });
    }
  });
});
</script>

<template>
  <div>
    <!-- Conditionally render based on role -->
    <div v-if="role === 'PU Manager' || role === 'FF' || role === 'Unlock Team'">
      <div id="map" style="height: 100vh; width: 100%;"></div>
      <p v-if="role === 'Unlock Team'">Interactive map: Full access to modify the map data.</p>
      <p v-else>You can view the map and its fields.</p>
    </div>
    <div v-else>
      <p>You do not have access to modify the map data.</p>
    </div>
  </div>
</template>

<style scoped>
#map {
  width: 100%;
  height: 100vh;
  border: 2px solid #ddd; /* Adding a border for better visibility */
}

p {
  font-size: 1rem;
  color: #7f8c8d;
  text-align: center;
}
</style>
