<template>
	<v-app>
		<Header />

		<v-main>
			<router-view />
		</v-main>
	</v-app>
</template>

<script>
	import Header from './components/Header.vue';
	export default {
		name: 'App',

		components: {
			Header,
		},

		data: () => ({}),
	};
</script>

<style scoped lang="scss">
	.v-app-bar {
		height: 60px;
	}
</style>
