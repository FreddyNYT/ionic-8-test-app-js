<template>
   <ion-page>
      <ion-header>
         <ion-toolbar>
            <ion-title>Experimento Patronum! <ion-icon :icon="colorWand"></ion-icon></ion-title>
         </ion-toolbar>
      </ion-header>
      <ion-content :fullscreen="true">
         <ion-header collapse="condense">
            <ion-toolbar>
               <ion-title size="large">Tab 3</ion-title>
            </ion-toolbar>
         </ion-header>

         <ion-list>
            <ion-item>
               <ion-label>Expecto experimento</ion-label>
               <ion-icon :icon="colorWand" size="large"></ion-icon>
            </ion-item>
            <ion-item>
               <ion-toggle :checked="false" v-model="darkmode" @ion-change="toggleDarkMode();">Darkmode</ion-toggle>
            </ion-item>
            <ion-item>
               <ion-button @click="askPermission" :disabled="geoEnabled">Enable Geolocation</ion-button><br>
               <ion-button @click="calculateDistance" :disabled="!geoEnabled">Bereken Afstand tot Manneken Pis</ion-button>
            </ion-item>
            <ion-item>
               <ion-label>lat : {{ coords.latitude }} <br> lon : {{ coords.longitude }}</ion-label>
            </ion-item>

            <!-- Weergave van de berekende afstand -->
            <ion-item v-if="distance !== null">
               <ion-label>Afstand tot Manneken Pis: {{ distance.toFixed(2) }} km</ion-label>
            </ion-item>
         </ion-list>
      </ion-content>
   </ion-page>
</template>

<script setup>
import { ref } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonList, IonItem, IonLabel, IonIcon, IonToggle, IonButton } from '@ionic/vue';
import { colorWand, cafe, logoDiscord } from 'ionicons/icons';
import { Geolocation } from '@capacitor/geolocation';

const darkmode = ref(false);
const coords = ref({ latitude: 4, longitude: 50 });
const geoEnabled = ref(false);
const geoDisabled = ref(true);
const distance = ref(null);

const mannekenPisLat = 50.84500108085066;
const mannekenPisLon = 4.34998572176742;

const askPermission = async () => {
   const perm = await Geolocation.requestPermissions({ permissions: ["location"] });
   if (perm.location == 'granted') {
      geoDisabled.value = false;
      geoEnabled.value = true;
   }
};

const calculateDistance = async () => {
   // Haal de huidige locatie op voordat we de afstand berekenen
   let coordinates = await Geolocation.getCurrentPosition({
      enableHighAccuracy: true,
      timeout: 10000,
      maximumAge: 0
   });
   coords.value.latitude = coordinates.coords.latitude;
   coords.value.longitude = coordinates.coords.longitude;

   // Bereken de afstand tot Manneken Pis
   const userLat = coords.value.latitude;
   const userLon = coords.value.longitude;
   distance.value = getDistanceFromLatLonInKm(userLat, userLon, mannekenPisLat, mannekenPisLon);
};

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

function deg2rad(deg) {
   return deg * (Math.PI / 180);
}

const toggleDarkMode = () => {
   console.log(`darkmode : ${darkmode.value}`)
};
</script>

<style scoped>
ion-icon {
   color: #5B8;
}
</style>
