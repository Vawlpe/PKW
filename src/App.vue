<template>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
</template>

<script setup lang="ts">
import { IonApp, IonRouterOutlet } from '@ionic/vue';
</script>

<style setup lang="scss">
:global(*) {
  padding:0 !important;
  margin:0 !important;
  padding-inline: 0 !important;
  margin-inline: 0 !important;
  --padding-start: 0 !important;
  --padding-end: 0 !important;
  --inner-padding-start: 0 !important;
  --inner-padding-end: 0 !important;
}
</style>
