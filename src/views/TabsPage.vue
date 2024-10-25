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

      <!-- Voeg een knop toe om de afstand te berekenen -->
      <div style="text-align: center; margin-top: 16px;">
         <ion-button @click="calculateDistance">Bereken Afstand tot Manneken Pis</ion-button>
      </div>
   </ion-page>
</template>

<script setup>
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet, IonButton } from '@ionic/vue';
import { addCircle, listOutline, constructSharp } from 'ionicons/icons';
import { toastController } from '@ionic/vue';

// Coördinaten van Manneken Pis
const mannekenPisLat = 50.84500108085066;
const mannekenPisLon = 4.34998572176742;

// Functie om afstand te berekenen
const calculateDistance = async () => {
   try {
      // Vraag de huidige locatie van het apparaat op
      navigator.geolocation.getCurrentPosition(async (position) => {
         const userLat = position.coords.latitude;
         const userLon = position.coords.longitude;

         // Bereken de afstand in meters
         const distance = getDistanceFromLatLonInKm(userLat, userLon, mannekenPisLat, mannekenPisLon) * 1000;

         // Toon een toast met de afstand
         const toast = await toastController.create({
            message: `Afstand tot Manneken Pis: ${distance.toFixed(2)} meter`,
            duration: 3000,
            position: 'top'
         });
         await toast.present();
      });
   } catch (error) {
      console.error("Error getting location", error);
   }
};

// Hulpfunctie om afstand tussen twee coördinaten te berekenen
function getDistanceFromLatLonInKm(lat1, lon1, lat2, lon2) {
   const R = 6371; // Straal van de aarde in km
   const dLat = deg2rad(lat2 - lat1);
   const dLon = deg2rad(lon2 - lon1);
   const a = Math.sin(dLat / 2) * Math.sin(dLat / 2) +
      Math.cos(deg2rad(lat1)) * Math.cos(deg2rad(lat2)) *
      Math.sin(dLon / 2) * Math.sin(dLon / 2);
   const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
   return R * c; // Afstand in km
}

// Converteert graden naar radialen
function deg2rad(deg) {
   return deg * (Math.PI / 180);
}
</script>
