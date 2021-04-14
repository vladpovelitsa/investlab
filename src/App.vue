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

		data: () => ({
			options: {
				chart: {
					id: 'vuechart-example',
				},
				xaxis: {
					categories: [1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998],
				},
			},
			series: [
				{
					name: 'series-1',
					data: [30, 40, 45, 50, 49, 60, 70, 91],
				},
			],
		}),
	};
</script>

<style scoped lang="scss">
	.v-app-bar {
		height: 60px;
	}
</style>
