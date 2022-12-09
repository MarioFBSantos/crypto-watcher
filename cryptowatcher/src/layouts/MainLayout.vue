<template>
	<div>
		<Navbar />
		<Topper />
		<Glitch class="logo" />
		<router-view />
	</div>
</template>

<script lang="ts">
	import { Vue, Component } from 'vue-property-decorator';
	import Index from '../pages/Index.vue';
	import Navbar from '../components/navbar.vue';
	import Topper from '../components/topper.vue';
	import Glitch from '../components/glitch.vue';

	@Component({
		components: { Index, Navbar, Topper, Glitch },
	})
	export default class MainLayout extends Vue {}
</script>

<style lang="scss" scoped>
	.logo {
		position: relative;
		top: -145px;

		display: flex;
		justify-content: center;
		margin: auto;
	}
</style>
