<template>
<ion-accordion :value="system.id" toggle-icon-slot="start">
  <ion-item slot="header">
    <ion-card class="sys-card" :style="{border: `4px double #${system.color}`}">
      <ion-card-header style="min-height: 4em;">
        <img v-if="system.banner" :src="system.banner" class="sys-banner"/>
        <div v-else class="sys-banner"/>
        <ion-card-title>
          <img v-if="system.avatar_url" :src="system.avatar_url" class="sys-avatar"/>
          <div v-else class="sys-avatar" :style="{padding:'0', backgroundColor: `#${system.color ? system.color : '000000'}`, border: `4px solid #${system.color ? system.color : '000000'}`}"></div>
          <ion-text class="sys-name">{{ system.name }}</ion-text>
          <ion-text class="sys-id"><ion-icon :icon="atOutline"/> ({{ system.id }})</ion-text>
          <div/>
          <div style="display: flex; flex-direction: column; justify-content: space-between;">
            <ion-text v-if="system.pronouns" class="sys-pronouns"><ion-icon :icon="transgenderOutline"/> {{ system.pronouns }}</ion-text>
            <ion-text v-else class="sys-pronouns"><ion-icon :icon="transgenderOutline"/> [No Pronouns]</ion-text>
            <ion-text v-if="system.tag" class="sys-pronouns"><ion-icon :icon="pricetag"/> {{ system.tag }}</ion-text>
            <ion-text v-else class="sys-pronouns"><ion-icon :icon="pricetag"/> [No Tag]</ion-text>
          </div>
          <ion-text v-if="system.color" class="sys-color" :style="{backgroundColor: `#${system.color}`}"><ion-icon :icon="colorPalette"/> #{{ system.color }}</ion-text>
          <ion-text v-else class="sys-color" style="background-color:black"><ion-icon :icon="colorPalette"/> [No Color]</ion-text>
        </ion-card-title>
      </ion-card-header>
    </ion-card>
  </ion-item>
  <div class="sys-desc" slot="content">
    <div >{{ system.description }}</div>
    <ion-card>
      <ion-card-header style="min-height: 2em;">
        <ion-text class="sys-name" style="color:white; padding: 0.5rem 1rem 0.5rem 1rem; font-size: large;">Members</ion-text>
      </ion-card-header>
      <ion-card-content>
        <ion-accordion-group>
          <MemberAccordion v-for="mem in system.members" :member="mem[1]" />
        </ion-accordion-group>
      </ion-card-content>
    </ion-card>
  </div>
</ion-accordion>
</template>

<script setup lang="ts">
import { IonIcon, IonCard, IonCardHeader, IonCardContent, IonCardTitle, IonItem, IonText, IonAccordion, IonAccordionGroup } from '@ionic/vue';
import { pricetag, transgenderOutline, calendarNumber, colorPalette, atOutline } from 'ionicons/icons';
import MemberAccordion from '@/components/Member/MemberAccordion.vue';
import { defineProps } from 'vue';

const props = defineProps(['system']);
</script>

<style scoped lang="scss">
:global(ion-icon) {
  margin-inline: -.5ch .5ch !important;
}
ion-card {
  padding: 0 !important;
  margin: 0 !important;
  margin-inline: 0 !important;
  &.sys-card {
    height: 6rem;
    width: 100%;
    ion-card-header {
      padding:0;
      margin:0;

      .sys-banner {
        opacity: 45%;
      }

      ion-card-title {
        position: absolute;
        display: grid;
        grid-template-columns: 65px 15ch 10ch;
        grid-template-rows: 1.2ch 0.75em;
        grid-gap: 1ch;
      }
    }
  }
  .sys-desc {
    margin: 1em !important;
  }

  .sys-avatar {
    overflow: hidden;
    border-radius: 50%; 
    width:64px;
    height: 64px;
    object-fit: cover;
    padding:0.4em;
    box-sizing: border-box;
  }
  .sys-name {
    font-size: 72%;
    padding-top: 0.25em;
    text-shadow: 1px 1px 2px #f38ba8, 0 0 1em #89b4fa, 0 0 0.2em #89b4fa;
  }
  .sys-id, .sys-pronouns, .sys-color {
    font-size: small;
  }
  .sys-id {
    padding-top:0.75em;
  }

  .sys-color {
    margin-top: 0.5rem;
    text-align: center;
    align-self:center;
    border-radius: 10px;
    color: var(--ion-color-dark);
    text-shadow: 1px 1px 2px var(--ion-color-light), 0 0 1em var(--ion-color-light), 0 0 0.2em var(--ion-color-light);
  }

  ion-card-content {
    padding: 0;
  }
}

ion-accordion {
  ion-item {
    --padding-start: 0.5em;
    &:hover, &:hover>ion-card {
      background-color: var(--ion-color-light);
    }
  }
}
</style>
