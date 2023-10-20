<script setup>
import { ref, onMounted } from "vue";
import { useRoute, RouterLink } from "vue-router";
import axios from "axios";

const apiData = ref([]);
const routeParam = ref(useRoute().params.param);
</script>

<template>
  <div class="home">
    <h2>Accueil</h2>
  </div>
</template>

<style scoped></style>
