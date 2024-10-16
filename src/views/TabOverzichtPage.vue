<template>
	<ion-page>
		<ion-header>
			<ion-toolbar>
				<ion-title>Producten</ion-title>
			</ion-toolbar>
		</ion-header>
		<ion-content :fullscreen="true">
			<ion-header collapse="condense">
				<ion-toolbar>
					<ion-title size="large">Tab 2</ion-title>
				</ion-toolbar>
			</ion-header>

			<!-- We zorgen er hier voor dat de pr_id getoond wordt 'on hover' -->
			<!-- Kan je de product categorie id tonen wanneer over de categorienaam wordt 'gehoverd' ?-->
			<ion-list>
				<ion-item v-for="{ pr_id, pr_prijs, pr_naam, ct_naam } in producten" :key="pr_id">
					<ion-item slot="start">€{{ pr_prijs }}</ion-item>
					<ion-label :title="pr_id">{{ pr_naam }}</ion-label>
					<ion-item slot="end">{{ ct_naam }}</ion-item>
				</ion-item>

			</ion-list>
		</ion-content>
	</ion-page>
</template>

<script setup>
import { ref } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonList, IonLabel, IonItem } from '@ionic/vue';

const producten = ref([
	{ pr_id: 1, pr_naam: "Banaan", pr_prijs: 1.50, ct_naam: "fruit", pr_ct_id: 1 },
	{ pr_id: 2, pr_naam: "Spruitjes", pr_prijs: 3.50, ct_naam: "groente", pr_ct_id: 2 },
	{ pr_id: 3, pr_naam: "Sinaasappel", pr_prijs: 1.00, ct_naam: "fruit", pr_ct_id: 1 },
	{ pr_id: 4, pr_naam: "Sinaasbanaan", pr_prijs: 2.00, ct_naam: "fruit", pr_ct_id: 1 },
	{ pr_id: 5, pr_naam: "Sinaaspeer", pr_prijs: 3.00, ct_naam: "fruit", pr_ct_id: 1 },
	{ pr_id: 6, pr_naam: "Appelflap", pr_prijs: 3.50, ct_naam: "groente", pr_ct_id: 2 },
]);

</script>