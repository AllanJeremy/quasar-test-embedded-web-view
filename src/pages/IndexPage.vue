<!-- eslint-disable @typescript-eslint/no-explicit-any -->
<script setup lang="ts">
import { ref, onMounted } from 'vue';

// This will hold the event we need to trigger the install prompt
const deferredPrompt = ref<Event | null>(null);
const isInstallable = ref(false);

onMounted(() => {
  window.addEventListener('beforeinstallprompt', (e) => {
    // Prevent the mini-infobar from appearing on mobile
    e.preventDefault();
    // Save the event so it can be triggered later.
    deferredPrompt.value = e;
    // Update UI to notify the user they can install the PWA
    isInstallable.value = true;
  });
});

const installPWA = async () => {
  if (deferredPrompt.value) {
    // Show the install prompt
    (deferredPrompt.value as any).prompt();
    // Wait for the user to respond to the prompt
    const { outcome } = await (deferredPrompt.value as any).userChoice;
    if (outcome === 'accepted') {
      console.log('User accepted the install prompt');
    } else {
      console.log('User dismissed the install prompt');
    }
    deferredPrompt.value = null;
    isInstallable.value = false;
  }
};
</script>

<template>
  <section class="q-pa-lg">
    <q-btn v-if="isInstallable" @click="installPWA">Install App</q-btn>
  </section>
</template>
