<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <div>
    <nav class="navbar">
      <ul>
        <li><RouterLink to="/">Accueil</RouterLink></li>
        <li><RouterLink to="/about">À propos</RouterLink></li>
        <li><RouterLink to="/contact">Contact</RouterLink></li>
      </ul>
    </nav>
    <RouterView />
  </div>
</template>

<style scoped></style>
