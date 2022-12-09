<template>
	<div class="nav">
		<router-link class="tile logo" :to="`/`">CW</router-link>
		<router-link class="logo-link tile" :to="`/crypto`"
			>Cryptos
		</router-link>
		<router-link class="logo-link tile" :to="`/market`"
			>Market
		</router-link>
	</div>
</template>

<script lang="ts">
	import { Vue, Component } from 'vue-property-decorator';

	@Component({
		components: {},
	})
	export default class Navbar extends Vue {}
</script>

<style lang="scss" scoped>
	.logo {
		font-size: 1.6em;
	}
	.nav {
		position: fixed;
		right: 0;
		top: 50%;

		display: flex;
		flex-direction: column;

		z-index: 999;
		opacity: 0.6;
		transition: 0.3s;
	}
	.nav:hover {
		opacity: 1;
	}

	.tile {
		padding: 25px;
		color: white;
		text-decoration: none;
		background-color: #2f3c5d;
	}
</style>
