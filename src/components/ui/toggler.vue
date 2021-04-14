<template>
	<label class="d-flex align-items-center toggler">
		<slot name="input">
			<input
				type="checkbox"
				class="visually_hidden"
				name="model"
				@change="checked = !checked"
			/>
		</slot>
		<span class="toggler__text">
			<slot name="text"> Lorem ipsum dolor sit amet. </slot>
		</span>
		<span
			class="toggler__indicator"
			:class="checked ? 'toggler__indicator--active' : ''"
		>
			<span></span>
		</span>
	</label>
</template>

<script>
	export default {
		name: 'toggler',
		props: {
			model: {
				type: Boolean,
				required: true,
			},
		},
		data() {
			return {
				checked: false,
			};
		},
		methods: {},
	};
</script>

<style scoped lang="scss">
	.toggler {
		cursor: pointer;
		&__text {
			font-size: 12px;
			color: #95aac9;
			margin-right: 6px;
		}
		&__indicator {
			width: 40px;
			height: 22px;
			position: relative;
			background: #95aac9;
			border-radius: 11px;
			display: flex;
			align-items: center;
			span {
				display: block;
				background: #fff;
				width: 16px;
				height: 16px;
				border-radius: 50%;
				transition: 0.3s;
				position: absolute;
				top: 50%;
				left: 4px;
				transform: translate(0, -50%);
			}
			&--active {
				background: #2c7be5;
				span {
					left: calc(100% - 4px);
					transform: translate(-100%, -50%);
				}
			}
		}
	}
</style>
