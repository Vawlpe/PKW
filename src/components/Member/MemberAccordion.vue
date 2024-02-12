<template>
<ion-accordion :value="member.id" style="height:fit-content" toggle-icon-slot="start">
  <ion-item slot="header"><ion-card class="mem-card">
    <ion-card-header>
      <img v-if="member.banner" :src="member.banner" class="mem-banner"/>
      <ion-card-title>
        <img v-if="member.avatar_url" :src="member.avatar_url" class="mem-avatar" :style="{padding:'0', border: `4px solid #${member.color}`}"/>
        <div v-else class="mem-avatar" :style="{padding:'0', backgroundColor: `#${member.color ? member.color : '000000'}`, border: `4px solid #${member.color ? member.color : '000000'}`}"/>
          <ion-text v-if="member.display_name" class="mem-name">{{ member.display_name }}</ion-text>
          <ion-text v-else class="mem-name">{{ member.name }}</ion-text>
          <ion-text v-if="member.display_name" class="mem-id"><ion-icon :icon="atOutline"/> ({{ member.name }}: {{ member.id }})</ion-text>
          <ion-text v-else class="mem-id"><ion-icon :icon="atOutline"/> ({{ member.id }})</ion-text>
        <div/>
        <div style="display: flex; flex-direction: column; justify-content: space-between;">
          <ion-text v-if="member.pronouns" class="mem-pronouns"><ion-icon :icon="transgenderOutline"/> {{ member.pronouns }}</ion-text>
          <ion-text v-else class="mem-pronouns"><ion-icon :icon="transgenderOutline"/> [No Pronouns]</ion-text>
          <ion-text>
            <ion-text v-if="member.birthday" class="mem-pronouns">
              <ion-icon :icon="calendarNumber"/> {{ new Date(member.birthday).toLocaleDateString() }}
            </ion-text>
            <ion-text v-else class="mem-pronouns">
              <ion-icon :icon="calendarNumber"/> [No DOB]
            </ion-text>
            <ion-text v-if="member.proxy_tags && member.proxy_tags.length > 0" class="mem-pronouns" style="position: absolute; overflow: visible; padding-top: 0.25rem;">
              <ion-icon :icon="pricetag" style="padding-left:1rem;"/> {{ member.proxy_tags.flatMap((e:any) => { return `${e.prefix ? e.prefix : ''}text${e.suffix ? e.suffix : ''}` }).join(", ")}}
            </ion-text>
            <ion-text v-else class="mem-pronouns" style="position: absolute; overflow: visible; padding-top: 0.4rem; text-align: center;">
              <ion-icon :icon="pricetag" style="padding-left:1rem;"/> [No Proxy-tags]
            </ion-text>
          </ion-text>
        </div>
        <ion-text v-if="member.color" class="mem-color" :style="{backgroundColor: `#${member.color}`}"><ion-icon :icon="colorPalette"/> #{{ member.color }}</ion-text>
        <ion-text v-else class="mem-color" style="background-color:black"><ion-icon :icon="colorPalette"/> [No Color]</ion-text>
      </ion-card-title>
    </ion-card-header>
  </ion-card></ion-item>
  <div class="sys-desc" slot="content">{{ member.description }}</div>
 </ion-accordion>
</template>

<script setup lang="ts">
  import { IonIcon, IonCard, IonCardHeader, IonCardContent, IonCardTitle, IonItem, IonText, IonAccordion } from '@ionic/vue';
  import { pricetag, transgenderOutline, calendarNumber, colorPalette, atOutline } from 'ionicons/icons';
  import { defineProps } from 'vue';

  const props = defineProps(['member'])
</script>

<style scoped lang="scss">
ion-card {
  padding: 0 !important;
  margin: 0 !important;
  margin-inline: 0 !important;
  
  &.mem-card {
    height:5rem;
    width: 100%;
    
    ion-card-header {
      padding:0;
      margin:0;

      .mem-banner {
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
  
  .mem-avatar {
    overflow: hidden;
    border-radius: 50%; 
    width:64px;
    height: 64px;
    object-fit: cover;
    padding:0.4em;
    box-sizing: border-box;
  }
  .mem-name {
    font-size: 72%;
    padding-top: 0.25em;
    text-shadow: 1px 1px 2px #f38ba8, 0 0 1em #89b4fa, 0 0 0.2em #89b4fa;
  }
  .mem-id, .mem-pronouns, .mem-color {
    font-size: small;
  }
  .mem-id {
    padding-top:0.75em;
  }

  .mem-color {
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
</style>
