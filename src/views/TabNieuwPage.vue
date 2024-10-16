<template>
	<ion-page>
		<ion-header>
			<ion-toolbar>
				<ion-title>Voeg een product toe</ion-title>
			</ion-toolbar>
		</ion-header>
		<ion-content :fullscreen="true">
			<ion-header collapse="condense">
				<ion-toolbar>
					<ion-title size="large">Voeg een product toe</ion-title>
				</ion-toolbar>
			</ion-header>
			<ion-grid>
				<ion-row>
					<ion-col class="ion-text-center">Welk product wil je toevoegen?</ion-col>
				</ion-row>

				<ion-row>
					<ion-col>
						<ion-item>
							<ion-input label="Product" label-placement="stacked" placeholder="Naam product"
								v-model="productNaam" required="true" @ion-blur="logProduct()"></ion-input>
						</ion-item>
						<ion-item>
							<ion-input label="Prijs" label-placement="stacked" placeholder="10.00" v-model="productPrijs"
								type="number" required="true" @ion-blur="logProduct()"></ion-input>
						</ion-item>
						<ion-item>
							<ion-select label="Categorie" label-placement="stacked" interface="popover"
								placeholder="Selecteer categorie" v-model="productCategorie" @ion-change="logProduct()">
								<ion-select-option value="0" disabled="true">Welk type product?</ion-select-option>
								<ion-select-option value="1">Fruit</ion-select-option>
								<ion-select-option value="2">Groente</ion-select-option>
							</ion-select>
						</ion-item>
					</ion-col>
				</ion-row>
				<ion-row>
					<ion-col>
						<ion-button expand="block" @click="verzendProduct()">Bevestig</ion-button>
					</ion-col>
				</ion-row>
			</ion-grid>

		</ion-content>
	</ion-page>
</template>

<script setup>
import { ref, inject } from 'vue'
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonGrid, IonRow, IonCol, IonItem, IonInput, IonSelect, IonSelectOption, IonButton } from '@ionic/vue';

const productNaam = ref('');
const productPrijs = ref(0.00);
const productCategorie = ref(0);

const axios = inject('axios') // inject axios
const postProduct = () => {
	axios
		.post('https://stevenop.be/wm/api2/products/', {
			PR_naam: productNaam.value,
			PR_CT_ID: productCategorie.value,
			PR_prijs: productPrijs.value
		})
		.then(response => {
			// controleer de response
			console.log(response);
			if (response.status !== 200) {
				// TODO: er is iets fout gegaan, doe iets met deze info
				// mogelijk met https://ionicframework.com/docs/api/toast
				console.log(response.status);
			} else {
				// maak de velden leeg
				productNaam.value = '';
				productPrijs.value = '0.0';
				productCategorie.value = 0;
				//TODO: Bevestig dat het product is toegevoegd
				// mogelijk met https://ionicframework.com/docs/api/toast
			}
		});
}
const logProduct = () => {
	console.log(`naam: ${productNaam.value}, prijs: ${productPrijs.value}, categorie: ${productCategorie.value}`);
};

const verzendProduct = () => {
	// TODO: input controle indien nodig

	// verstuur naar de backend (API)
	postProduct();
};
</script>