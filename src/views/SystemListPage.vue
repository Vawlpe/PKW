<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title style="padding-left: 2ch;">System</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true" color="light">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large" style="padding-left: 1rem;">System</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-card>
        <ion-card-title>Add System</ion-card-title>
        <ion-button :disabled="!addSysForm.canSubmit" @click="addSysForm_submit"
                    style="position:absolute; right:.5rem; top:.5rem;" 
        >+</ion-button>
        <ion-input id='addSysForm.id' ref="addSysForm.id.elem" :value="addSysForm.id.model" @ionInput="ionicInputChange"
                   label="ID:"   placeholder="Enter system ID"  
        />
        <ion-input id='addSysForm.token' ref="addSysForm.token.elem" :value="addSysForm.token.model" @ionInput="ionicInputChange"
                   label="Token" placeholder="Enter optional token to view private info & edit system"
        />
      </ion-card>
      <ion-card>
        <ion-card-header>
          <ion-card-title>Saved Systems</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          <ion-accordion-group>
            <SystemAccordion v-for="s in saved_systems" :system="s.sys"/>
          </ion-accordion-group>
        </ion-card-content>
      </ion-card>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
  import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCard, IonInput, IonButton, IonCardHeader, IonCardContent, IonCardTitle, IonItem, IonAccordion, IonAccordionGroup } from '@ionic/vue';
import SystemAccordion from '@/components/System/SystemAccordion.vue';
import PKAPI, { System } from 'pkapi.js';
import { ref } from 'vue';

const addSysForm = ref({
  id: {
    elem: ref(),
    model: ref('')
  },
  token: {
    elem: ref(),
    model: ref('')
  },
  canSubmit: ref(false)
})
const saved_systems = ref<{id:string,token?:string,api:PKAPI,sys:System|undefined}[]>([]);

const DEBUG = true;
if (DEBUG) load_system('exmpl');

async function load_system(id:string, token?:string) {
  let new_sys:{id:string,token?:string,api:PKAPI,sys:System|undefined} = {
    id: id,
    token: token,
    api: new PKAPI({
      version: 2,
      user_agent: 'PKWorld/0.0.0 (github.com/vawlpe)',
      token: token
    }),
    sys: undefined
  };

  new_sys.sys = await new_sys.api.getSystem({system: new_sys.id});
  new_sys.sys.members = await new_sys.api.getMembers({system: new_sys.id});
  saved_systems.value.push(new_sys);
  if (DEBUG) console.log(new_sys.sys.members);
}

function addSysForm_submit(e:any) {
  load_system(addSysForm.value.id.model, addSysForm.value.token.model);
  addSysForm.value = {
    id: {
      elem: ref(),
      model: ''
    },
    token: {
      elem: ref(),
      model: ''
    },
    canSubmit: false
  };
}

const ionicInputChange = (ev:any) => {
  const elem = ev.target;
  const value = elem.value;
  addSysForm.value[ev.target.id == "addSysForm.id" ? "id" : "token"].model = value;

  if (elem.value !== undefined) {
    elem.value = value;
  }
  addSysForm.value.canSubmit = addSysForm.value.id.model.length > 0;
}
</script>

<style scoped lang="scss">
ion-card {
  margin: 1ch;
  ion-card-content {
    padding: 0;
  }
}
</style>
