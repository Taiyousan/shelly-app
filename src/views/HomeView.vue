<script setup>
import { ref, onMounted } from "vue";

const apiData = ref([]);

onMounted(async () => {
  const response = await fetch("http://192.168.1.100/shelly");
  apiData.value = await response.json();
  console.log(apiData.value);
});
</script>

<template>
  <div class="api-results">
    <h2>Résultats de l'API</h2>

    <!-- Affichage des clés et valeurs du résultat -->
    <ul>
      <li v-for="(value, key) in apiData" :key="key">
        <strong>{{ key }}:</strong> {{ value }}
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
