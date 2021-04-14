<template>
	<v-app-bar app color="#132A46" dark>
		<v-container>
			<v-row align="center">
				<v-col cols="1" sm="4"></v-col>
				<v-col cols="5" sm="4" align="center">
					<router-link :to="{ name: 'home' }">
						<img src="./../assets/img/logo.svg" width="130" />
					</router-link>
				</v-col>
				<v-col cols="5" sm="4">
					<router-link :to="{ name: 'login' }" class="d-flex justify-end">
						<img src="./../assets/img/avatar.png" width="40" height="40" />
					</router-link>
				</v-col>
			</v-row>
		</v-container>
	</v-app-bar>
</template>

<script>
	export default {
		name: 'Header',

		data: () => ({}),
	};
</script>

<style>
	.v-app-bar.v-app-bar--fixed {
		z-index: 99 !important;
	}
</style>
