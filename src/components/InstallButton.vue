<script setup>
import { ref, onMounted } from 'vue';

const showInstallButton = ref(false);
let deferredPrompt = null;

onMounted(() => {
  window.addEventListener('beforeinstallprompt', (event) => {
    event.preventDefault();
    deferredPrompt = event;
    showInstallButton.value = true;
  });

  window.addEventListener('appinstalled', () => {
    showInstallButton.value = false;
    deferredPrompt = null;
  });
});

async function installApp() {
  if (!deferredPrompt) return;

  deferredPrompt.prompt();

  const { outcome } = await deferredPrompt.userChoice;

  if (outcome === 'accepted') {
    showInstallButton.value = false;
  }

  deferredPrompt = null;
}
</script>

<template>
  <button v-if="showInstallButton" class="install-button" @click="installApp">
    Instalar aplicativo
  </button>
</template>

<style scoped>
.install-button {
  display: block;
  width: 100%;
  padding: 14px;
  margin-top: 20px;
  background-color: #27ae60;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.2s;
}

.install-button:hover {
  background-color: #219a52;
}
</style>
