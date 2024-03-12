<template>
  <q-page class="row items-center justify-evenly">
    <div class="column q-gutter-y-lg">
      <q-btn outlined to="/another">Vue router go to other</q-btn>
      <q-btn color="primary" @click="goToExternalLink('/another')"
        >External (window.replace)</q-btn
      >
      <q-btn color="positive" @click="goToExternalLink('/another', true)"
        >External new tab (window.open)</q-btn
      >
      <q-btn color="negative" @click="attemptToTriggerSystemBrowser('/another')"
        >External new tab (window.open(link, '_system'))</q-btn
      >
    </div>
  </q-page>
</template>

<script setup lang="ts">
function attemptToTriggerSystemBrowser(link: string) {
  window.open(link, '_system');
}
function goToExternalLink(link: string, isNewTab = false) {
  if (isNewTab) {
    window.open(link, '__blank');
  }

  return window.location.replace(link);
}
</script>
