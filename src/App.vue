<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
    <div class="wrapper">
      <HelloWorld/>
    </div>
  </header>

  <main class="center">
    <TheWelcome />
  </main>
</template>

<style scoped>
  .center {
    align-items: center;
  }
</style>
