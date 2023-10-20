<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

const apiData = ref([]);
const routeParam = ref(useRoute().params.param);

onMounted(async () => {
  const response = await fetch(`"http://192.168.1.100/${routeParam}"`);
  apiData.value = await response.json();
  console.log(apiData.value);
});
</script>

<template>
  <div class="api-results">
    <h2>Résultats de l'API</h2>
    <p>Paramètre de l'URL: {{ routeParam }}</p>

    <!-- Affichage des clés et valeurs du résultat -->
    <ul>
      <li v-for="(value, key) in apiData" :key="key">
        <strong>{{ key }}:</strong> {{ value }}
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
