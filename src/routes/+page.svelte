<script lang="ts">
	import { gaussianPos, initialPos } from '$lib/utilities/particlePosition';
	const LF = 64;
	const LA = 192;
	const BF = 426;

	let particles: HTMLDivElement[] = [];

	const handleMouseEnter = () => {
		for (const k in particles) {
			const l = parseInt(particles[k].style.left.replace('px', ''));
			const b = parseInt(particles[k].style.bottom.replace('px', ''));

			const dx = (gaussianPos[k].x - initialPos[k].x) * LF;
			const dy = (gaussianPos[k].y - initialPos[k].y) * BF;
			particles[k].style.left = `${l + dx}px`;
			particles[k].style.bottom = `${b + dy}px`;
		}
	};

	const handleMouseLeave = () => {
		for (const k in particles) {
			particles[k].style.left = `${initialPos[k].x * LF + LA}px`;
			particles[k].style.bottom = `${initialPos[k].y * BF}px`;
		}
	};
</script>

<div class="flex h-full w-full min-h-screen bg-[#222831]">
	<div
		on:mouseenter={handleMouseEnter}
		on:mouseleave={handleMouseLeave}
		class="relative mx-auto my-auto h-64 w-96 rounded-lg bg-slate-100 hover:bg-slate-900 transition-all duration-300 shadow-lg group"
	>
		<!-- {#each [...gaussianPos,...initialPos] as gp,ip}
			<div
				style="left:{gp.x * 64 + 192}px ; bottom: {gp.y * 577 + 5}px ;"
				class="absolute shadow h-1 w-1 rounded-full bg-teal-800 group-hover:translate-x-10 transition-all"
			/>
		{/each} -->
		<!-- {#each gaussianPos as gp}
			<div
				style="left:{gp.x * 64 + 192}px ; bottom: {gp.y * 577 + 5}px ;"
				class="absolute shadow h-1 w-1 rounded-full bg-teal-800 group-hover:translate-x-10 transition-all"
			/>
		{/each} -->
		{#each Object.entries(initialPos) as [k, ip]}
			<!-- {@const gp = gaussianPos[parseInt(k)]}
			{@const dx = (gp.x - ip.x) * LF}
			{@const dy = (gp.y - ip.y) * BF} -->
			<div
				bind:this={particles[k]}
				style="left:{ip.x * LF + LA}px ; bottom: {ip.y * BF}px ;"
				class="absolute shadow h-1 w-1 rounded-full bg-teal-800 group-hover:bg-teal-100 transition-all duration-700"
			/>
		{/each}
	</div>
</div>
