<script setup>
import {
    computed,
    defineProps,
} from 'vue';

const props = defineProps({
  role: String,
  searchQuery: String,
});

// Sample farmer data
const farmers = [
  { id: 1, name: 'Islas' },
  { id: 2, name: 'Maria' },
  { id: 3, name: 'Laila' },
];

// Computed property for filtering
const filteredFarmers = computed(() => {
  return farmers.filter(f => f.name.toLowerCase().includes(props.searchQuery.toLowerCase()));
});
</script>

<template>
  <aside class="sidebar">
    <h2>Farmers</h2>
    <ul>
      <li v-for="farmer in filteredFarmers" :key="farmer.id">{{ farmer.name }}</li>
    </ul>

    <div v-if="['Unlock Team', 'PU Manager', 'FF'].includes(role)">
      <p><strong>Full access</strong> to manage data.</p>
    </div>
    <div v-else-if="role === 'Project Manager'">
      <p><strong>Dashboard access</strong>, can visualize polygons.</p>
    </div>
    <div v-else-if="role === 'Auditor'">
      <p><strong>View-only access</strong>.</p>
    </div>
    <div v-else>
      <p><strong>Dashboard visualization only</strong>.</p>
    </div>
  </aside>
</template>
