<template>
  <Suspense>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="map" href="/app/map">
          <ion-icon aria-hidden="true" :icon="triangle" />
          <ion-label>Map</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="system" href="/app/system">
          <ion-icon aria-hidden="true" :icon="ellipse" />
          <ion-label>System</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="settings" href="/app/settings">
          <ion-icon aria-hidden="true" :icon="square" />
          <ion-label>Settings</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</Suspense>
</template>

<script setup lang="ts">
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet } from '@ionic/vue';
import { ellipse, square, triangle } from 'ionicons/icons';
</script>
