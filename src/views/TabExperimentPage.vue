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
					<ion-toggle :checked="false" name="coffeeMode" class="coffee">Coffee mode <ion-icon
							:icon="cafe"></ion-icon></ion-toggle>
				</ion-item>
				<ion-item>
					<ion-toggle :checked="false" name="discordMode" class="discord">Discord mode <ion-icon
							:icon="logoDiscord"></ion-icon></ion-toggle>
				</ion-item>
				<ion-item>
					<ion-button @click="askPermission" :disabled="geoEnabled">Enable Geolocation</ion-button><br>
					<ion-button @click="getLocation" :disabled="geoDisabled">Haal locatie op</ion-button>
				</ion-item>
				<ion-item>
					<ion-label>lat : {{ coords.latitude }} <br> lon : {{ coords.longitude }}</ion-label>
				</ion-item>


			</ion-list>

		</ion-content>
	</ion-page>
</template>

<script setup>
import { ref } from 'vue'
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonList, IonItem, IonLabel, IonIcon, IonToggle, onIonViewDidEnter, onIonViewDidLeave, onIonViewWillEnter, onIonViewWillLeave, IonButton } from '@ionic/vue';
import { colorWand, cafe, logoDiscord } from 'ionicons/icons';
import { Geolocation } from '@capacitor/geolocation';

const darkmode = ref(false);
const coords = ref({ latitude: 4, longitude: 50 });
const geoEnabled = ref(false);
const geoDisabled = ref(true);

const askPermission = async () => {
	// vraag voor de location permission
	const perm = await Geolocation.requestPermissions({ permissions: ["location"] });
	console.log("permission :");
	console.log(perm);
	if (perm.location == 'granted') {
		geoDisabled.value = false;
		geoEnabled.value = true;
	}
};

const getLocation = async () => {
	// gaal de locatie op;

	let coordinates = await Geolocation.getCurrentPosition(
		{
			enableHighAccuracy: true,
			timeout: 10000,
			maximumAge: 0
		});
	coords.value.latitude = coordinates.coords.latitude;
	coords.value.longitude = coordinates.coords.longitude;
};

const toggleDarkMode = () => {
	console.log(`darkmode : ${darkmode.value}`)
};


// demo van een aantal event-hooks in Ionic 
onIonViewDidEnter(() => {
	console.log('Experimento View did enter');
});

onIonViewDidLeave(() => {
	console.log('Experimento View did leave');
});

onIonViewWillEnter(() => {
	console.log('Experimento View will enter');
});

onIonViewWillLeave(() => {
	console.log('Experimento View will leave');
});

</script>


<style scoped>
ion-icon {
	color: #5B8;
}

.coffee ion-icon {
	color: #6F4E37;
}

.discord ion-icon {
	color: purple;
}
</style>