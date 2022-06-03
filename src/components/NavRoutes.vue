<script setup>
import { RouterLink } from 'vue-router';

</script>
<template>
     <header>

    <div class="navbar navbar-expand-lg navbar-light bg-light">
        <nav class="navbar-nav">
        <RouterLink class="nav-item nav-link" to="/">Home</RouterLink>
        <RouterLink class="nav-item nav-link" to="/register">Register</RouterLink>
      </nav>
    </div>
  </header>
</template>