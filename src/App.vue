<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <div>
    <nav class="navbar">
      <ul>
        <li><RouterLink to="/">Accueil</RouterLink></li>
        <li><RouterLink to="/api">API</RouterLink></li>
      </ul>
    </nav>
    <RouterView />
  </div>
</template>

<style scoped></style>
