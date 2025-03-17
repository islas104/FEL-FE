<script setup>
import {
    computed,
    defineProps,
} from 'vue';

const props = defineProps({
  role: {
    type: String,
    required: true
  },
  searchQuery: {
    type: String,
    required: true
  }
});

// Sample farmer data (replace with API integration as needed)
const farmers = [
  { id: 1, name: 'Islas' },
  { id: 2, name: 'Maria' },
  { id: 3, name: 'Laila' }
];

// Filter farmers based on the search query (case-insensitive)
const filteredFarmers = computed(() => {
  return farmers.filter((farmer) =>
    farmer.name.toLowerCase().includes(props.searchQuery.toLowerCase())
  );
});
</script>

<template>
  <aside class="sidebar">
    <h2>Farmers</h2>
    <ul>
      <li v-for="farmer in filteredFarmers" :key="farmer.id">
        {{ farmer.name }}
      </li>
    </ul>

    <div class="access-info">
      <template v-if="['Unlock Team', 'PU Manager', 'FF'].includes(role)">
        <p><strong>Full access</strong> to manage data.</p>
      </template>
      <template v-else-if="role === 'Project Manager'">
        <p><strong>Dashboard access</strong>, can visualize polygons.</p>
      </template>
      <template v-else-if="role === 'Auditor'">
        <p><strong>View-only access</strong>.</p>
      </template>
      <template v-else>
        <p><strong>Dashboard visualization only</strong>.</p>
      </template>
    </div>
  </aside>
</template>

<style scoped>
.sidebar {
  width: 250px;
  background-color: #f8f9fa;
  padding: 20px;
  border-right: 1px solid #ddd;
}
.sidebar h2 {
  font-size: 1.2rem;
  margin-bottom: 10px;
}
.sidebar ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
.sidebar li {
  padding: 8px 0;
  border-bottom: 1px solid #eee;
}
.access-info {
  margin-top: 20px;
  font-size: 0.9rem;
}
</style>
