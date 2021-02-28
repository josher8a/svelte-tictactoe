<script type="text/javascript">
	let grid = new Array(9).fill(null);
	let result = null;
	let turn = "❌";

	function reset() {
		grid = new Array(9).fill(null);
		result = null;
		turn = "❌";
	}
	reset();
	const index = (i, j) => j + i * 3;

	const winningConditions = [
		[index(0, 0), index(0, 1), index(0, 2)],
		[index(1, 0), index(1, 1), index(1, 2)],
		[index(2, 0), index(2, 1), index(2, 2)],
		[index(0, 0), index(1, 0), index(2, 0)],
		[index(0, 1), index(1, 1), index(2, 1)],
		[index(0, 2), index(1, 2), index(2, 2)],
		[index(0, 0), index(1, 1), index(2, 2)],
		[index(0, 2), index(1, 1), index(2, 0)],
	];

	const isWin = () =>
		winningConditions.some((winningCondition) =>
			winningCondition
				.map((index) => grid[index])
				.reduce((eq, val) => (eq = val === eq ? eq : false))
		);

	const setValue = (i) => {
		grid[i] = turn;
		grid = [...grid];

		result = isWin() ? `${turn} WINS!` : null;
		if (grid.includes(null) || result) {
			turn = turn === "❌" ? "⭕" : "❌";
		} else {
			result = "👵 DRAW GAME";
		}
	};
</script>

<h1>{result ? result : `${turn} turns`}</h1>
<div>
	{#each grid as cell, i}
		<button on:click={() => (result ? reset() : cell ? cell : setValue(i))}>
			{result ? "🆕" : cell ? cell : ""}
		</button>
	{/each}
</div>

<style>
	div {
		display: grid;
		grid-template-columns: repeat(3, 20vmin);
		grid-template-rows: repeat(3, 20vmin);
		grid-gap: 1vmin;
		background: #000;
		margin: auto;
		width: 61vmin;
		height: 61vmin;
	}
	button {
		justify-self: stretch;
		align-self: stretch;
		width: 100%;
		height: 100%;
		margin: -0.5vmin 0 0 -0.5vmin;
		border: 0;
		padding: 0;
		font-size: 10vmin;
		background: #fff;
	}
	h1 {
		display: block;
		height: 15vmin;
		margin: auto;
		text-align: center;
		font-size: 10vmin;
	}
</style>
