<template>
  <q-page class="q-pa-xl items-center justify-evenly">
    <div class="column q-gutter-y-lg">
      <q-btn outlined to="/another">Vue router go to other</q-btn>
      <q-btn color="primary" @click="goToExternalLink('/another')"
        >External [window.replace]</q-btn
      >
      <q-btn color="positive" @click="goToExternalLink('/another', true)"
        >External new tab [window.open(link, '__blank')]</q-btn
      >
      <q-btn color="negative" @click="attemptToTriggerSystemBrowser('/another')"
        >External new tab [window.open(link, '_system')]</q-btn
      >

      <a class="q-btn bg-yellow-2" href="/another" target="__blank" download
        >Open in browser (link with download attr)</a
      >

      <q-btn color="dark" @click="replaceLocationHref('/another')"
        >Replacing window.location.href</q-btn
      >
      <q-btn
        color="dark"
        outline
        @click="
          replaceLocationHref(
            'https://quasar-test-embedded-web-view.vercel.app/another'
          )
        "
        >Replacing window.location.href (external link)</q-btn
      >
    </div>
    <hr class="q-my-xl" />
    <section class="q-mt-lg">
      <h6 class="q-my-none">Additional data</h6>

      <q-card>
        <q-card-section>
          <p class="text-overline">User agent: {{ userAgent }}</p>
          <p class="text-overline">Is Instagram: {{ userAgentIsInstagram }}</p>
        </q-card-section>
      </q-card>
    </section>
  </q-page>
</template>

<script setup lang="ts">
import { computed } from 'vue';

const userAgent = computed(() => navigator.userAgent);
const userAgentIsInstagram = computed(() =>
  navigator.userAgent?.includes('Instagram')
);

function attemptToTriggerSystemBrowser(link: string) {
  window.open(link, '_system');
}
function goToExternalLink(link: string, isNewTab = false) {
  if (isNewTab) {
    window.open(link, '__blank');
  }

  return window.location.replace(link);
}

function replaceLocationHref(link: string) {
  window.location.href = link;
}
</script>
