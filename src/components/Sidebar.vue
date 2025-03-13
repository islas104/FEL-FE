<script setup>
import { ref } from 'vue';

// Example farmer data
const farmers = ref([
  { id: 1, name: 'Islas' },
  { id: 2, name: 'Laila' },
  { id: 3, name: 'Maria' },
]);

// Role prop passed from parent
const props = defineProps({
  role: String,
});
</script>

<template>
  <aside class="sidebar">
    <h2>Farmers</h2>
    <ul>
      <li v-for="farmer in farmers" :key="farmer.id">{{ farmer.name }}</li>
    </ul>

    <!-- Role-based content -->
    <div v-if="role === 'Unlock Team'">
      <p>You have full access to manage farmers and data.</p>
    </div>
    <div v-else>
      <p>You can only view farmers' data.</p>
    </div>
  </aside>
</template>

<style scoped>
.sidebar {
  width: 250px;
  background-color: #34495e;
  color: white;
  padding: 1rem;
  height: 100vh;
  box-shadow: 2px 0px 10px rgba(0, 0, 0, 0.1);
}

h2 {
  font-size: 1.2rem;
  font-weight: 600;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 10px 0;
  font-size: 1rem;
}
</style>
