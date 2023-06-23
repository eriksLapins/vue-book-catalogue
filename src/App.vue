<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
      </nav>
      <RouterView />
    </div>
  </header>

  
</template>

<script>
  export default {
    name: 'App'
  }
</script>

<style scoped>

</style>
