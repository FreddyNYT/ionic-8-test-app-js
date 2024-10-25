<template>
   <ion-page>
      <ion-tabs>
         <ion-router-outlet></ion-router-outlet>
         <ion-tab-bar slot="bottom">
            <ion-tab-button tab="tab1" href="/tabs/tabnieuw">
               <ion-icon aria-hidden="true" :icon="addCircle" />
               <ion-label>Nieuw</ion-label>
            </ion-tab-button>

            <ion-tab-button tab="tab2" href="/tabs/tabOverzicht">
               <ion-icon aria-hidden="true" :icon="listOutline" />
               <ion-label>Overzicht</ion-label>
            </ion-tab-button>

            <ion-tab-button tab="tab3" href="/tabs/tabExperiment">
               <ion-icon aria-hidden="true" :icon="constructSharp" />
               <ion-label>Experimento</ion-label>
            </ion-tab-button>
         </ion-tab-bar>
      </ion-tabs>

      <!-- Voeg knoppen buiten de ion-tab-bar toe -->
      <div style="text-align: center; margin-top: 16px;">
         <ion-button>Default</ion-button>
         <ion-button shape="round">Round</ion-button>
      </div>
   </ion-page>
</template>

<script setup>
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet, IonButton } from '@ionic/vue';
import { addCircle, listOutline, constructSharp } from 'ionicons/icons';

// Iconen zijn uit verschillende Ionicons-sets gebruikt:
//  - addCircle (standaard)
//  - listOutline (Outline)
//  - constructSharp (Sharp)
// Voor consistentie kun je het beste één stijlset gebruiken in je project.
</script>
