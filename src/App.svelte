<script lang="ts">
	import { fly } from "svelte/transition";

	function sleep(ms) {
		return new Promise((resolve) => setTimeout(resolve, ms));
	}
	let click = 0;
	let upgraded_times = 1;
	async function clck() {
		click += upgraded_times;
		transformbass = rotated;
		await sleep(200);
		transformbass = normal;
	}
	function upgrade() {
		upgradeDis = true;
        upgraded_times +=1
	}
	const rotated = "rotate3d(-30,10,-10,30deg)";
	const normal = "rotate3d(0,0,0,0deg)";
	let transformbass = normal;
	let upgradeDis = true;
	$: {
		if (click >= upgraded_times * 50) {
			upgradeDis = false;
		}
	}
</script>

<svelte:window />
<main>
	<button class="seabs" on:click={() => clck()}>
		<img
			src="/seabass.webp"
			alt=""
			class="seab"
			style="transform: {transformbass}"
			draggable="false"
		/>
	</button>
	<div class="menu">
		<h1 class="slap">
			slaps:
			{#key click}
				<span style="display: inline-block" in:fly={{ y: -10 }}>
					{click}
				</span>
			{/key}
		</h1>
		<div>
			<button on:click={upgrade} class="upgrade" disabled={upgradeDis}
				>Upgrade</button
			>Click left:
			{#key click}
				<span style="display: inline-block" in:fly={{ y: 10 }}>
             {(((upgraded_times * 50) - click) <= 0) ? 0 : (upgraded_times * 50) - click}
				</span>
			{/key}
            <br>
            <span>Pointless and waste time😉</span>
		</div>
	</div>
</main>

<style>
	@import url("https://fonts.bunny.net/css2?family=Press+Start+2P&display=swap");
	main {
		display: grid;
		grid-template-columns: auto auto;
		padding: 10px;
		align-content: center;
		height: 100vh;
	}
	.seab {
		width: 50vw;
	}
	.seabs {
		background-color: transparent;
		border-style: none;
		cursor: url("/pointer.png"), auto;
	}
	.menu {
		margin-left: 5vw;
	}
	.upgrade {
		border-style: solid;
		border-color: brown;
	}
</style>
