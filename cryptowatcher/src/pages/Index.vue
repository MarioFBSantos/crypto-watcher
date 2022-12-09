<template>
	<div>
		<p class="introduce">
			Here you can check every cryptocurrency price and market
			flutuantions
		</p>
		<p class="text">
			Click on
			<router-link class="logo-link" :to="`/crypto`"
				>Cryptos
			</router-link>
			to check the 100 most popular cryptocurrencies at this moment, or
			click on
			<router-link class="logo-link" :to="`/market`">Market </router-link>
			to check what is trending at the market right now
		</p>


	</div>
</template>

<script lang="ts">
	import { Vue, Component } from 'vue-property-decorator';
	import Navbar from '../components/navbar.vue';
	import Glitch from '../components/glitch.vue';
	@Component({
		components: { Navbar, Glitch },
	})
	export default class PageIndex extends Vue {}
</script>

<style lang="scss" scoped>
	.text {
		font-size: 1.4em;
		width: 80%;
		position: relative;
		margin: auto;
		font-weight: 300;
		text-align: center;
	}
	.back {
		width: 100%;
		z-index: -10;
		display: block;
	}

	.card {
		background-color: #000;
		width: 30%;
		height: 50%;
		color: white;
		border-radius: 5px;
		padding: 50px;
		display: flex;
		flex-direction: column;
		flex-wrap: nowrap;
		align-items: center;
		font-size: 1.2em;
	}
	.containerCard {
		display: flex;
		gap: 5%;
		flex-direction: row;
		justify-content: space-evenly;
	}
	.button-link {
		background-color: rgb(253, 255, 253);
		text-decoration: none;
		border-radius: 8px;
		color: rgb(91, 91, 92);
	}
	p {
		font-size: 1.2em;
		font-weight: 300;
	}
	.introduce {
		font-weight: 400;
		font-size: 3.2em;
		text-align: center;
		padding-bottom: 50px;
	}
</style>
