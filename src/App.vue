<script setup>
import AppHeader from './components/AppHeader.vue';
import OfflineBanner from './components/OfflineBanner.vue';
import UpdatePrompt from './components/UpdatePrompt.vue';
</script>

<template>
  <OfflineBanner />
  <AppHeader />
  <main>
    <router-view />
  </main>
  <UpdatePrompt />
</template>

<style scoped>
main {
  padding-bottom: 40px;
}
</style>
