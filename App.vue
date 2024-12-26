<script setup>
import NavbarSection from './src/components/NavbarSection.vue'
import { RouterView } from 'vue-router'
</script>

<template>
  <div>
    <NavbarSection />
    <RouterView />
  </div>
</template>
