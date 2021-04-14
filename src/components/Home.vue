<template>
	<div>
		<v-container fluid class="main_chart">
			<v-container>
				<v-row>
					<v-col cols="6" sm="auto" align="left" class="mr-auto">
						<div class="main_chart__title">ИНВЕСТИЦИИ</div>
						<div class="main_chart__value">Статистика</div>
					</v-col>
					<v-col cols="6" sm="auto">
						<div class="main_chart__title">ИНВЕСТИЦИИ</div>
						<div class="main_chart__value">1 000.00 USD</div>
					</v-col>
					<v-col cols="6" sm="auto">
						<div class="main_chart__title">ИНВЕСТИЦИИ</div>
						<div class="main_chart__value">1 000.00 USD</div>
					</v-col>
					<v-col cols="6" sm="auto">
						<div class="main_chart__title">ИНВЕСТИЦИИ</div>
						<div class="main_chart__value">1 000.00 USD</div>
					</v-col>
				</v-row>
				<v-row>
					<v-col cols="12">
						<apexchart
							type="line"
							height="350"
							:options="chartOptions"
							:series="series"
						></apexchart>
					</v-col>
				</v-row>
			</v-container>
		</v-container>
		<v-container fluid class="page_content">
			<v-container>
				<v-row align="stretch">
					<v-col cols="12" class="page_content__grid">
						<div class="item">
							<header class="d-flex flex-wrap justify-space-between item__header pa-4">
								<div class="item__title">Сравнение</div>
								<Toggler @click="test" :model="compareColumns">
									<template v-slot:text> Сравнение с вашими показателями </template>
								</Toggler>
							</header>
							<div class="item__content">
								<apexchart
									type="bar"
									:options="chartOptionColumns"
									:series="seriesColumns"
								></apexchart>
							</div>
						</div>

						<div class="item">
							<header
								class="d-flex justify-space-between align-center item__header px-4"
							>
								<div class="item__title">Сравнение</div>
								<v-tabs class="ml-auto" align-self="end">
									<v-tab class="pa-0"> All </v-tab>
									<v-tab class="pa-0"> Direct </v-tab>
								</v-tabs>
							</header>
							<div class="item__content">
								<div class="donut_wrap">
									<apexchart
										type="donut"
										:options="chartOptionsDonut"
										:series="seriesDonut"
									></apexchart>
								</div>
							</div>
						</div>

						<div class="item">
							<div
								class="item__content d-flex flex-column align-center justify-center"
								v-if="!showTable"
							>
								<img src="../assets/img/not_found.png" alt="not found" class="mb-5" />
								<h6 class="text-h4 text-center">Доверительное управление</h6>
								<p class="text-body2 text-center">
									Наполнение портфеля из представленных инструментов.
								</p>
								<v-btn
									color="#2C7BE5"
									dark
									large
									@click.prevent="showTable = !showTable"
								>
									Наполнить
								</v-btn>
							</div>
							<div class="item__content" v-else-if="showTable">
								<header
									class="d-flex justify-space-between align-center item__header px-4 pb-4"
								>
									<div class="item__title">Доверительное управление</div>
									<v-btn color="white" small @click.prevent="showTable = !showTable">
										Добавить
									</v-btn>
								</header>
								<v-data-table
									:headers="headers"
									:items="items"
									disable-pagination
									:hide-default-footer="true"
									width="100%"
									full-width
								>
									<template template v-slot:item.bot="{ item }">
										<div class="d-flex align-center">
											<span
												class="bot_status mr-4"
												:style="
													item.status === 'green'
														? 'background-color: #00D97E'
														: item.status === 'red'
														? 'background-color: #F5D83E'
														: item.status === 'yellow'
														? 'background-color: #E63757'
														: ''
												"
											></span>
											{{ item.bot }}
										</div>
									</template>
									<template v-slot:item.percent="{ item }">
										<v-btn color="rgba(44,123,229,.1)" x-small>
											{{ item.percent }}
										</v-btn>
									</template>
									<template v-slot:item.actions="">
										<div class="d-flex justify-end">
											<v-btn color="gray" text class="ml-auto">
												<v-icon color="#C0CCDD"> mdi-dots-vertical </v-icon>
											</v-btn>
										</div>
									</template>
								</v-data-table>
							</div>
						</div>
						<div class="item item--activity">
							<header
								class="d-flex justify-space-between align-center item__header px-4"
							>
								<div class="item__title">Активность</div>
								<v-btn color="blue" text>
									<router-link :to="{ name: '#' }" class="text-decoration-none"
										>Все</router-link
									>
								</v-btn>
							</header>
							<div class="item__content">
								<ul class="activity_list">
									<li class="mb-8">
										<router-link :to="{ name: '#' }" class="text-decoration-none d-flex">
											<v-btn fab color="#e9f1fd" class="mr-4">
												<v-icon color="#2C7BE5"> mdi-email-outline </v-icon>
											</v-btn>
											<div>
												<h6 class="subtitle-2 font-weight-bold text--primary mb-2">
													Launchday 1.4.0 update email sent
												</h6>
												<p class="text-body-2 text--secondary font-weight-medium mb-0">
													Sent to all 1,851 subscribers
												</p>
												<time class="text--secondary text--disabled text-body-2">
													2m ago
												</time>
											</div>
										</router-link>
									</li>
									<li class="mb-8">
										<router-link :to="{ name: '#' }" class="text-decoration-none d-flex">
											<v-btn fab color="#e9f1fd" class="mr-4">
												<v-icon color="#2C7BE5"> mdi-email-outline </v-icon>
											</v-btn>
											<div>
												<h6 class="subtitle-2 font-weight-bold text--primary mb-2">
													Launchday 1.4.0 update email sent
												</h6>
												<p class="text-body-2 text--secondary mb-0 font-weight-medium">
													Sent to all 1,851 subscribers
												</p>
												<time class="text--secondary text--disabled text-body-2">
													2m ago
												</time>
											</div>
										</router-link>
									</li>
									<li class="mb-8">
										<router-link :to="{ name: '#' }" class="text-decoration-none d-flex">
											<v-btn fab color="#e9f1fd" class="mr-4">
												<v-icon color="#2C7BE5"> mdi-email-outline </v-icon>
											</v-btn>
											<div>
												<h6 class="subtitle-2 font-weight-bold text--primary mb-2">
													Launchday 1.4.0 update email sent
												</h6>
												<p class="text-body-2 text--secondary mb-0 font-weight-medium">
													Sent to all 1,851 subscribers
												</p>
												<time class="text--secondary text--disabled text-body-2">
													2m ago
												</time>
											</div>
										</router-link>
									</li>
									<li class="mb-8">
										<router-link :to="{ name: '#' }" class="text-decoration-none d-flex">
											<v-btn fab color="#e9f1fd" class="mr-4">
												<v-icon color="#2C7BE5"> mdi-email-outline </v-icon>
											</v-btn>
											<div>
												<h6 class="subtitle-2 font-weight-bold text--primary mb-2">
													Launchday 1.4.0 update email sent
												</h6>
												<p class="text-body-2 text--secondary mb-0 font-weight-medium">
													Sent to all 1,851 subscribers
												</p>
												<time class="text--secondary text--disabled text-body-2">
													2m ago
												</time>
											</div>
										</router-link>
									</li>
									<li class="mb-8">
										<router-link :to="{ name: '#' }" class="text-decoration-none d-flex">
											<v-btn fab color="#e9f1fd" class="mr-4">
												<v-icon color="#2C7BE5"> mdi-email-outline </v-icon>
											</v-btn>
											<div>
												<h6 class="subtitle-2 font-weight-bold text--primary mb-2">
													Launchday 1.4.0 update email sent
												</h6>
												<p class="text-body-2 text--secondary mb-0 font-weight-medium">
													Sent to all 1,851 subscribers
												</p>
												<time class="text--secondary text--disabled text-body-2">
													2m ago
												</time>
											</div>
										</router-link>
									</li>
									<li class="mb-0">
										<router-link :to="{ name: '#' }" class="text-decoration-none d-flex">
											<v-btn fab color="#e9f1fd" class="mr-4">
												<v-icon color="#2C7BE5"> mdi-email-outline </v-icon>
											</v-btn>
											<div>
												<h6 class="subtitle-2 font-weight-bold text--primary mb-2">
													Launchday 1.4.0 update email sent
												</h6>
												<p class="text-body-2 text--secondary mb-0 font-weight-medium">
													Sent to all 1,851 subscribers
												</p>
												<time class="text--secondary text--disabled text-body-2">
													2m ago
												</time>
											</div>
										</router-link>
									</li>
								</ul>
							</div>
						</div>
						<div class="item">
							<div class="item__content d-flex align-center" v-if="!showTable">
								<div>
									<h6 class="subtitle-1 font-weight-bold mb-4">
										Независимое управление для безопасной самостоятельной работы с
										инструментами
									</h6>
									<p class="subtitle-2 font-weight-regular mb-10">
										Наполнение портфеля из представленных инструментов.
									</p>
									<v-btn
										color="#2C7BE5"
										dark
										large
										@click.prevent="showTable = !showTable"
									>
										Наполнить
									</v-btn>
								</div>
								<img class="dance_img" src="../assets/img/dance.png" alt="dance" />
							</div>
							<div class="item__content" v-else-if="showTable">
								<header
									class="d-flex justify-space-between align-center item__header px-4 pb-4"
								>
									<div class="item__title">Доверительное управление</div>
									<v-btn color="white" small @click.prevent="showTable = !showTable">
										Добавить
									</v-btn>
								</header>
								<v-data-table
									:headers="headers"
									:items="items2"
									disable-pagination
									:hide-default-footer="true"
									width="100%"
									full-width
								>
									<template template v-slot:item.bot="{ item }">
										<div class="d-flex align-center">
											<span
												class="bot_status mr-4"
												:style="
													item.status === 'green'
														? 'background-color: #00D97E'
														: item.status === 'red'
														? 'background-color: #F5D83E'
														: item.status === 'yellow'
														? 'background-color: #E63757'
														: ''
												"
											></span>
											{{ item.bot }}
										</div>
									</template>
									<template v-slot:item.percent="{ item }">
										<v-btn
											color="rgba(44,123,229,.1)"
											x-small
											@click.prevent="showTable = !showTable"
										>
											{{ item.percent }}
										</v-btn>
									</template>
									<template v-slot:item.actions="">
										<div class="d-flex justify-end">
											<v-btn color="gray" text class="ml-auto">
												<v-icon color="#C0CCDD"> mdi-dots-vertical </v-icon>
											</v-btn>
										</div>
									</template>
								</v-data-table>
							</div>
						</div>
					</v-col>
				</v-row>
			</v-container>
		</v-container>
	</div>
</template>

<script>
	import Toggler from './ui/toggler';

	export default {
		name: 'Home',

		components: {
			Toggler,
		},
		data: () => ({
			series: [
				{
					name: 'Desktops',
					data: [
						6500,
						7000,
						8600,
						6500,
						7000,
						12000,
						14000,
						12900,
						12500,
						12000,
						11500,
						15000,
					],
				},
			],
			chartOptions: {
				chart: {
					height: 450,
					type: 'line',
					background: 'transparent',
					toolbar: false,
					redrawOnWindowResize: true,
				},
				dataLabels: {
					enabled: false,
				},
				legend: {
					markers: {
						strokeColor: '#000',
					},
				},
				stroke: {
					curve: 'smooth',
					colors: '#3075E3',
				},
				title: {
					text: '',
				},
				grid: {
					strokeDashArray: 3,
					row: {
						colors: ['#fff', 'transparent'], // takes an array which will be repeated on columns
						opacity: 0,
					},
					borderColor: 'rgba(255,255,255,.1)',
				},
				theme: {
					mode: 'dark',
				},
				yaxis: {
					labels: {
						style: {
							colors: '#6E84A3',
						},
					},
					crosshairs: {
						show: false,
					},
				},

				xaxis: {
					crosshairs: {
						show: false,
					},
					categories: [
						'Jan',
						'Feb',
						'Mar',
						'Apr',
						'May',
						'Jun',
						'Jul',
						'Aug',
						'Sep',
						'Oct',
						'Nov',
						'Dec',
					],
					labels: {
						style: {
							colors: '#6E84A3',
						},
					},
					axisBorder: {
						show: false,
					},
					axisTicks: {
						show: false,
					},
				},
				responsive: [
					{
						breakpoint: 960,
						options: {
							chart: {
								height: 300,
							},
						},
					},
					{
						breakpoint: 600,
						options: {
							chart: {
								height: 200,
							},
						},
					},
				],
			},

			seriesColumns: [
				{
					name: '2020',
					data: [44, 55, 57, 56, 61, 58, 63, 60, 66],
				},
				{
					name: '2021',
					data: [76, 85, 101, 98, 87, 105, 91, 114, 94],
				},
			],
			chartOptionColumns: {
				colors: ['#2C7BE5', '#D2DDEC'],

				chart: {
					type: 'bar',
					height: 450,
					redrawOnWindowResize: true,
					toolbar: false,
				},
				plotOptions: {
					bar: {
						horizontal: false,
						columnWidth: '40%',
						borderRadius: 5,
					},
				},
				dataLabels: {
					enabled: false,
				},
				stroke: {
					show: true,
					width: 2,
					colors: ['transparent'],
				},
				xaxis: {
					categories: [
						'Feb',
						'Mar',
						'Apr',
						'May',
						'Jun',
						'Jul',
						'Aug',
						'Sep',
						'Oct',
					],
					colors: ['#000', '#fff'],
					labels: {
						style: {
							colors: '#6E84A3',
						},
					},
				},
				yaxis: {
					labels: {
						style: {
							colors: '#6E84A3',
						},
					},
				},
				fill: {
					opacity: 1,
				},
				tooltip: {
					y: {
						formatter: function (val) {
							return '$ ' + val + ' тыс.';
						},
					},
				},
				responsive: [
					{
						breakpoint: 2900,
						options: {
							chart: {
								height: 500,
							},
						},
					},
					{
						breakpoint: 1900,
						options: {
							chart: {
								height: 250,
							},
						},
					},
					{
						breakpoint: 1264,
						options: {
							chart: {
								height: 200,
							},
						},
					},
				],
			},

			seriesDonut: [70, 15, 15],
			chartOptionsDonut: {
				chart: {
					type: 'donut',
				},
				labels: ['Cryptobot', 'Neirbot', 'Newbot'],
				colors: ['#2c7be5', '#a6c5f7', '#d2ddec'],
				dataLabels: {
					enabled: false,
				},
				legend: {
					position: 'bottom',
				},
				plotOptions: {
					pie: {
						donut: {
							size: '80%',
						},
					},
				},
				responsive: [
					{
						breakpoint: 960,
						options: {
							chart: {
								width: 300,
							},
							legend: {
								position: 'bottom',
							},
						},
					},
					{
						breakpoint: 420,
						options: {
							chart: {
								width: 250,
							},
						},
					},
				],
			},

			compareColumns: false,
			showTable: false,
			headers: [
				{ text: 'БОТ', value: 'bot', sortable: false },
				{ text: 'ДОХОД', value: 'income', sortable: false },
				{ text: 'ПРОЦЕНТ', value: 'percent', sortable: false },
				{ text: 'ТЕСТЫ', value: 'tests', sortable: false },
				{ text: '', value: 'actions', sortable: false },
			],
			items: [
				{
					bot: 'Homepage',
					income: '97,028',
					percent: '25.5%',
					tests: '2:14',
					actions: '',
					status: 'green',
				},
				{
					bot: 'Blog',
					income: '97,028',
					percent: '25.5%',
					tests: '2:14',
					actions: '',
					status: 'yellow',
				},
				{
					bot: 'My Account',
					income: '97,028',
					percent: '25.5%',
					tests: '2:14',
					actions: '',
					status: 'red',
				},
				{
					bot: 'Why Dashkit',
					income: '97,028',
					percent: '25.5%',
					tests: '2:14',
					actions: '',
					status: 'green',
				},
				{
					bot: 'Documentation',
					income: '97,028',
					percent: '25.5%',
					tests: '2:14',
					actions: '',
					status: 'yellow',
				},
			],
			items2: [
				{
					bot: 'Homepage',
					income: '97,028',
					percent: '25.5%',
					tests: '2:14',
					actions: '',
					status: 'green',
				},
				{
					bot: 'Blog',
					income: '97,028',
					percent: '25.5%',
					tests: '2:14',
					actions: '',
					status: 'yellow',
				},
				{
					bot: 'My Account',
					income: '97,028',
					percent: '25.5%',
					tests: '2:14',
					actions: '',
					status: 'red',
				},
			],
		}),
		methods: {
			test() {
				alert('1');
			},
		},
		mounted() {},
	};
</script>

<style lang="scss" scoped>
	.main_chart {
		background: #12263f;
		&__title {
			color: #6e84a3;
			font-size: 10px;
			font-weight: 700;
			margin-bottom: 4px;
			text-transform: uppercase;
			text-align: center;
		}

		&__value {
			font-size: 17px;
			font-weight: 700;
			color: #fff;
		}
	}
	.page_content__grid {
		margin-top: -55px;
		display: grid;
		grid-template-columns: 1.75fr 1fr;
		grid-gap: 24px;
		.item {
			background-color: #fff;
			border: 1px solid #e3ebf6;
			border-radius: 20px;
			height: 100%;
			&__header {
				height: 50px;
				// padding: 20px 25px;
				border-bottom: 1px solid #edf2f9;
				.v-slide-group__wrapper {
					flex: unset;
				}
				.v-tabs {
					width: auto;
					flex: unset;
					.v-tab {
						min-width: unset;
						width: fit-content;
						margin-left: 20px;
						text-transform: none;
					}
				}
			}
			&__title {
				color: #1f2d3d;
				font-size: 15px;
				font-weight: 700;
			}
			&__content {
				padding: 20px 20px;
				&:only-child {
					height: 100%;
				}
			}

			&--activity {
				grid-row: 2 / 4;
				grid-column: 2 / 3;
			}
		}
	}
	.activity_list {
		list-style: none;
		padding-left: 0;
		li {
			position: relative;
			z-index: 5;
			.v-btn {
				z-index: 5;
				position: relative;
				background: #000;
			}
			&:before {
				content: '';
				display: block;
				position: absolute;
				left: 28px;
				top: 20px;
				width: 1px;
				height: 125%;
				background: #e4ebf6;
				z-index: -1;
			}
			&:last-of-type:before {
				display: none;
			}
		}
	}
	.bot_status {
		display: block;
		width: 5px;
		height: 5px;
		border-radius: 50%;
		background-color: #000;
	}

	@media screen and (max-width: 1264px) {
		.page_content__grid {
			grid-template-columns: 1.25fr 1fr;

			.item {
				&__content {
					padding: 10px;
				}
			}
		}
	}
	@media screen and (max-width: 960px) {
		.page_content__grid {
			grid-template-columns: 1fr;

			.item {
				&--activity {
					grid-row: unset;
					grid-column: unset;
				}
			}
		}
		.donut_wrap {
			display: flex;
			justify-content: center;
			margin: auto;
		}
	}
	@media screen and (max-width: 750px) {
		.dance_img {
			display: none;
		}
	}
</style>
