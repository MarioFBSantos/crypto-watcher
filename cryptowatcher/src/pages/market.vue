<template>
	<div>
		<div class="guide">Market</div>

		<div v-for="(index, count) in marketList" :key="count" class="list">
			<div class="item q-pa-lg q-mt-md">
				<div class="top q-mb-md">
					<div>
						<div class="text-h6">{{ index.baseSymbol }}</div>
						<div class="text-subtitle3">{{ index.baseId }}</div>
					</div>
					<p class="rank">{{ index.rank }}</p>
				</div>
				<div class="infos">
					<div class="cells">
						<p class="header">Quote price</p>
						{{ decimals(index.priceQuote) }}
					</div>

					<div class="cells">
						<p class="header">USD price</p>
						{{ decimals(index.priceUsd) }}
					</div>

					<div class="cells">
						<p class="header">Volume 24Hrs</p>
						{{ decimals(index.volumeUsd24Hr) }}
					</div>

					<div class="cells">
						<p class="header">Percent Volume</p>
						% {{ decimals(index.percentExchangeVolume) }}
					</div>
					<!-- {{ index }} -->
				</div>
				<div class="text-subtitle2 footer q-mt-md">
					<div>
						Exchange:
						<q-btn
							target="_blank"
							:href="`https://${index.exchangeId}.com`"
							flat
							color="primary"
							>{{ index.exchangeId }}</q-btn
						>
					</div>
					Currency:
					{{ index.quoteSymbol }}
				</div>
			</div>
			<q-linear-progress
				indeterminate
				rounded
				track-color="black"
				color="purple"
				class="q-mt-sm"
			/>
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
		marketList: marketInfo = {
			exchangeId: '',
			rank: '',
			baseSymbol: '',
			baseId: '',
			quoteSymbol: '',
			quoteId: '',
			priceQuote: '',
			priceUsd: '',
			volumeUsd24Hr: '',
			percentExchangeVolume: '',
			tradesCount24Hr: '',
			updated: 0,
		};

		decimals(arg1: string) {
			const transform = +arg1;
			return transform.toFixed(2);
		}

		get items() {
			axios
				.get('https://api.coincap.io/v2/markets')
				.then((response) => {
					this.marketList = response.data.data;
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
	.list:nth-child(even) {
		background: rgb(248, 248, 248);
	}

	.list:nth-child(odd) {
		background: rgb(236, 236, 236);
	}

	.guide {
		font-size: 3.2em;

		display: flex;
		justify-content: center;
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
