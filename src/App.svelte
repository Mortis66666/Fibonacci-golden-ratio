<script lang="ts">
    const colors = [
			"red",
			"orange",
			"yellow",
			"green",
			"blue",
			"indigo",
			"purple"
		];
    const len = colors.length;

	let fib: number[] = [];
	let spam = false;
	let delay = 100;
	let val;
	$: l = fib.length;
	$: golden_ratio = fib[l-1] / fib[l-2];

	function add_num() {
		if (l < 2) {
			fib = [...fib, l];
		} else {
			fib = [...fib, fib[l-2] + fib[l-1]];
		}
	}


	function clear_num() {
		fib = [];
	}

	function determine_color(i: number): String {
		return colors[i%len];
	}

	function start_spam() {
		spam = true;
		val = setInterval(add_num, delay);
	}

	function stop_spam() {
		spam = false;
		clearInterval(val);
	}

</script>

<main>

	<h1>Fibonacci:</h1>

	<button on:click={add_num}>
		Add number
	</button>
	
	<button on:click={clear_num}>
		Clear
	</button>
	
	{#if !spam}
	<button on:click={start_spam}>
		Spam
	</button>
	{:else}
	<button on:click={stop_spam}>
		Stop
	</button>
	<p class="delay">Spam delay (ms): </p>
	<input type="number" bind:value={delay} name="delay">
	{/if}



	<p class="gr">Golder ratio: {golden_ratio}</p>
	<ul>
		{#each fib as n, i}
		<li style="color: {determine_color(i)}">{n}</li>
		{/each}
	</ul>


</main>

<style lang="scss">
	@mixin black-bg {
		background-color: black;
		color: white;
	}
	:root {
		@include black-bg();
	}
	h1 {
		@include black-bg();
	}
	.delay {
		@include black-bg();
	}
	.gr {
		font-size: 30px;
		color: gold;
	}
</style>