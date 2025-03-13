<script setup>
import { ref } from 'vue';

import MapView from './MapView.vue';
import Sidebar from './Sidebar.vue';

// Set initial role (this can be dynamically set from login or auth)
const role = ref('Unlock Team');

// Dynamic field data (can be fetched from API)
const fields = ref([
  { id: 1, boundary: [[51.505, -0.09], [51.51, -0.1], [51.52, -0.08]] },
  { id: 2, boundary: [[51.49, -0.1], [51.50, -0.12], [51.48, -0.08]] },
]);

// Center coordinates for the map
const center = ref([51.505, -0.09]);

// Method to change the role
const changeRole = (newRole) => {
  role.value = newRole;
};
</script>

<template>
  <div>
    <!-- Header Section -->
    <header class="header">
      <h1>Field Mapping System</h1>
    </header>

    <!-- Role Selector Buttons (at the top) -->
    <div class="role-buttons">
      <button @click="changeRole('Unlock Team')">Unlock Team</button>
      <button @click="changeRole('PU Manager')">PU Manager</button>
      <button @click="changeRole('FF')">Field Facilitator</button>
      <button @click="changeRole('Better Cotton')">Better Cotton</button>
      <button @click="changeRole('Auditor')">Auditor</button>
    </div>

    <div class="layout">
      <!-- Sidebar with role-based content -->
      <Sidebar :role="role" />
      
      <!-- Content Area: MapView -->
      <div class="content">
        <MapView :role="role" :fields="fields" :center="center" />
      </div>
    </div>

    <!-- Display the current role (for debugging) -->
    <p class="current-role">Current Role: {{ role }}</p>
  </div>
</template>

<style scoped>
/* General Page Layout */
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: #f4f6f9;
}

/* Header Section */
.header {
  background-color: #2c3e50;
  color: white;
  padding: 1rem;
  text-align: center;
  font-size: 2rem;
}

/* Role Buttons at the Top */
.role-buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 20px;
  margin-bottom: 20px;
}

button {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 12px 20px;
  font-size: 1rem;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #2980b9;
}

/* Layout */
.layout {
  display: flex;
  flex-direction: row;
  height: calc(100vh - 120px); /* Adjusted for header and button space */
}

.content {
  flex: 1;
  background-color: #ecf0f1;
  padding: 20px;
  overflow-y: auto;
}

/* Sidebar Styling */
.sidebar {
  width: 250px;
  background-color: #34495e;
  color: white;
  padding: 1rem;
  height: 100%;
  box-shadow: 2px 0px 10px rgba(0, 0, 0, 0.1);
}

.sidebar h2 {
  font-size: 1.2rem;
  font-weight: 600;
}

.sidebar ul {
  list-style-type: none;
  padding: 0;
}

.sidebar li {
  margin: 10px 0;
  font-size: 1rem;
}

/* Styling for the current role */
.current-role {
  text-align: center;
  margin-top: 20px;
  font-size: 16px;
  color: #7f8c8d;
}
</style>
