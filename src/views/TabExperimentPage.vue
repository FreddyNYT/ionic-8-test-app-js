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


			</ion-list>

		</ion-content>
	</ion-page>
</template>

<script setup>
import { ref } from 'vue'
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonList, IonItem, IonLabel, IonIcon, IonToggle, onIonViewDidEnter, onIonViewDidLeave, onIonViewWillEnter, onIonViewWillLeave } from '@ionic/vue';
import { colorWand, cafe, logoDiscord } from 'ionicons/icons';

const darkmode = ref(false);

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