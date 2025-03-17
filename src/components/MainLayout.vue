<script setup>
import { ref } from 'vue';

import MapView from './MapView.vue';
import Sidebar from './Sidebar.vue';

// Set up role state with a default role
const role = ref('Unlock Team');

// Sample fields data (replace with API integration as needed)
const fields = ref([
  { id: 1, boundary: [[51.505, -0.09], [51.51, -0.1], [51.52, -0.08]] },
  { id: 2, boundary: [[51.49, -0.1], [51.50, -0.12], [51.48, -0.08]] }
]);

const center = ref([51.505, -0.09]);

// Search query with debounce
const searchQuery = ref('');
let debounceTimeout = null;
const updateSearch = (event) => {
  clearTimeout(debounceTimeout);
  debounceTimeout = setTimeout(() => {
    searchQuery.value = event.target.value;
  }, 300);
};

// Change the current role
const changeRole = (newRole) => {
  role.value = newRole;
};
</script>

<template>
  <div class="app-container">
    <!-- Header -->
    <header class="header">
      <h1>Field Mapping System</h1>
    </header>

    <!-- Role Selector -->
    <div class="role-selector">
      <button
        v-for="r in ['Unlock Team', 'PU Manager', 'FF', 'Better Cotton', 'Project Manager', 'Auditor']"
        :key="r"
        :class="{ active: role === r }"
        @click="changeRole(r)"
      >
        {{ r }}
      </button>
    </div>

    <!-- Search Bar -->
    <div class="search-bar">
      <input
        type="text"
        @input="updateSearch"
        placeholder="🔍 Search farmers or fields..."
      />
    </div>

    <!-- Layout: Sidebar + Map -->
    <div class="layout">
      <Sidebar :role="role" :searchQuery="searchQuery" />
      <div class="content">
        <MapView :role="role" :fields="fields" :center="center" />
      </div>
    </div>

    <!-- Debugging / Info -->
    <p class="current-role">
      Current Role: <strong>{{ role }}</strong>
    </p>
  </div>
</template>

<style scoped>
/* Overall Container */
.app-container {
  font-family: sans-serif;
}

/* Header styling */
.header {
  background-color: #2c3e50;
  color: white;
  padding: 1.5rem;
  text-align: center;
  font-size: 2rem;
  font-weight: bold;
}

/* Role Selector styling */
.role-selector {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin: 15px 0;
}
.role-selector button {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 10px 18px;
  font-size: 1rem;
  border-radius: 5px;
  cursor: pointer;
  transition: transform 0.3s ease-in-out;
}
.role-selector button.active {
  background-color: #2980b9;
  font-weight: bold;
}
.role-selector button:hover {
  background-color: #2471a3;
  transform: scale(1.05);
}

/* Search Bar styling */
.search-bar {
  text-align: center;
  margin-bottom: 10px;
}
.search-bar input {
  width: 80%;
  padding: 10px;
  font-size: 1rem;
  border: 2px solid #ccc;
  border-radius: 5px;
}

/* Layout styling */
.layout {
  display: flex;
  height: calc(100vh - 190px);
}
.content {
  flex: 1;
  background-color: #ecf0f1;
  padding: 20px;
}

/* Current Role info */
.current-role {
  text-align: center;
  margin-top: 10px;
  font-size: 1rem;
}
</style>
