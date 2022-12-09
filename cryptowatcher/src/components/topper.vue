<template>
	<div>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			viewBox="0 0 1440 220"
			class="back"
		>
			<path
				fill="#000"
				fill-opacity="1"
				d="M0,192L48,165.3C96,139,192,85,288,85.3C384,85,480,139,576,160C672,181,768,171,864,149.3C960,128,1056,96,1152,96C1248,96,1344,128,1392,144L1440,160L1440,0L1392,0C1344,0,1248,0,1152,0C1056,0,960,0,864,0C768,0,672,0,576,0C480,0,384,0,288,0C192,0,96,0,48,0L0,0Z"
			></path>
		</svg>
	</div>
</template>

<script lang="ts">
	import { Vue, Component } from 'vue-property-decorator';

	@Component({
		components: {},
	})
	export default class Topper extends Vue {}
</script>

<style lang="scss" scoped>
	.back {
		width: 100%;
		z-index: -10;
		display: block;
	}
</style>
