<template>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="tab1" href="/tabs/tabnieuw">
          <ion-icon aria-hidden="true" :icon="addCircle" />
          <ion-label>Tab 1</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="tab2" href="/tabs/tabOverzicht">
          <ion-icon aria-hidden="true" :icon="listOutline" />
          <ion-label>Tab 2</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="tab3" href="/tabs/tabExperiment">
          <ion-icon aria-hidden="true" :icon="constructSharp" />
          <ion-label>Tab 3</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script setup>
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet } from '@ionic/vue';
import { addCircle, listOutline, constructSharp } from 'ionicons/icons';

// In dit voorbeeld zijn icons gebruikt uit de 3 Ionicons sets:
//  standaard of filled (addCircle)
//  Outline (listOutline)
//  Sharp (constructSharp)
// Voor consistentie blijf je in je eigen project best in 1 set.
// Let op : de syntax op https://ionic.io/ionicons/ volgt een ander patroon ("-" concatenatie)
//  add-circle online -> addCircle in je project
//  list-outline -> listOutline in je project
//  construct-sharp -> constructSharp in je project
</script>
