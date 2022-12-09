<template>
	<div>
		<div class="guide">Cryptos</div>
		<div
			v-for="(index, count) in marketList.data"
			:key="count"
			class="list"
		>
			<div class="item q-pa-lg q-mt-md">
				<div class="top q-mb-md">
					<div>
						<div class="text-h6">{{ index.symbol }}</div>
						<div class="text-subtitle3">{{ index.name }}</div>
					</div>
					<p class="rank">{{ index.rank }}</p>
				</div>
				<div class="infos">
					<div class="cells">
						<p class="header">Suplly</p>
						{{ decimals(index.supply) }}
					</div>

					<div class="cells">
						<p class="header">Max Suplly</p>
						{{ decimals(index.maxSupply) }}
					</div>

					<div class="cells">
						<p class="header">Market Cap</p>
						${{ decimals(index.marketCapUsd) }}
					</div>

					<div class="cells">
						<p class="header">Volume 24Hrs (USD)</p>
						${{ decimals(index.volumeUsd24Hr) }}
					</div>
					<!-- {{ index }} -->
				</div>
				<div class="text-subtitle2 footer q-mt-md">
					<div>Price (USD): ${{ decimals(index.priceUsd) }}</div>
					<div>
						Last 24 hours change:
						<span
							class="percent"
							:class="{ green: index.changePercent24Hr > 0 }"
							>% {{ decimals(index.changePercent24Hr) }}</span
						>
					</div>
				</div>
			</div>
			<div
				class="bar"
				:class="{ barGreen: index.changePercent24Hr > 0 }"
			></div>
		</div>
	</div>
</template>

<script lang="ts">
	import { Vue, Component } from 'vue-property-decorator';
	import axios from 'axios';

	export interface marketInfo {
		exchangeId: string;
		rank: string;
		baseSymbol: string;
		baseId: string;
		quoteSymbol: string;
		quoteId: string;
		priceQuote: string;
		priceUsd: string;
		volumeUsd24Hr: string;
		percentExchangeVolume: string;
		tradesCount24Hr: string;
		updated: number;
	}

	@Component({
		components: {},
	})
	export default class Market extends Vue {
		marketList = {};

		decimals(arg1: string | number) {
			let transform: number;

			if (arg1) {
				typeof arg1 === 'string'
					? (transform = +arg1)
					: (transform = arg1);
				return transform.toFixed(2);
			}

			return 'none';
		}

		get items() {
			axios
				.get('https://api.coincap.io/v2/assets')
				.then((response) => {
					this.marketList = response.data;
				})
				.catch((error) => console.log('err', error));

			return this.marketList;
		}

		get eachItem() {
			return this.marketList;
		}

		mounted() {
			this.items;
			console.log(this.eachItem);
		}
	}
</script>

<style lang="scss" scoped>
	.bar {
		width: 100%;
		height: 5px;
		background-color: red;
	}
	.barGreen {
		background-color: green;
	}
	.guide {
		font-size: 3.2em;

		display: flex;
		justify-content: center;
	}

	.percent {
		color: red;
	}
	.green {
		color: green;
	}

	.list:nth-child(even) {
		background: rgb(248, 248, 248);
	}

	.list:nth-child(odd) {
		background: rgb(236, 236, 236);
	}

	.list {
		width: 80%;
		position: relative;
		margin: auto;
	}

	.text-subtitle3 {
		color: #666;
	}

	.infos {
		display: flex;
		justify-content: space-around;
	}

	.footer {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.top {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}
	.cells {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.header {
		font-weight: 800;
	}

	.rank {
		font-size: 1.4em;
	}
</style>
