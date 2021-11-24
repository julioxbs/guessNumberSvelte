<script>
	let numberGuess;
	let random;
	let isTrue = false;
	let isVictory = false;
	let score;
	let highScore = 0;

	function randomNumber() {
		random = Math.trunc(Math.random() * 20 + 1);
		score = Math.trunc(Math.random() * 5 + 1);
	}

	randomNumber();

	function isTheSame() {
		if (numberGuess > 20) {
			alert("Write the number valid");
			numberGuess = "";
		}

		if (numberGuess === random) {
			isTrue = true;
			isVictory = true;
			document.querySelector("body").classList.add("victory");
		}

		numberGuess < random
			? (document.querySelector(".message").textContent = "To Low")
			: (document.querySelector(".message").textContent = "To High");

		// Clear Input
		document.querySelector(".guess").value = "";
	}

	function restartGame() {
		isTrue = !isTrue;
		isVictory = !isVictory;
		document.querySelector("body").classList.remove("victory");
		highScore += score;
		randomNumber();
	}
</script>

<header>
	<h1>Guess My Number!</h1>
	<p class="between">(Between 1 and 20)</p>
	<button on:click={restartGame} class="btn again">Again!</button>

	{#if isTrue}
		<div class="number">{numberGuess}</div>
	{:else}
		<div class="number">?</div>
	{/if}
</header>
<main>
	<section class="left">
		{#if !isTrue}
			<input
				bind:value={numberGuess}
				type="number"
				class="guess"
				max="20"
			/>
			<button on:click={isTheSame} type="button" class="btn check"
				>Check!</button
			>
		{/if}
	</section>

	<section class="right">
		{#if isVictory}
			<p class="message">Congratulations 🎉🎉</p>
			<p class="label-score">
				💯 Score: <span class="score">{score}</span>
			</p>
		{:else}
			<p class="message">Starting guess...</p>
			<p class="label-score">💯 Score: <span class="score">0</span></p>
		{/if}

		<p class="label-highscore">
			🥇 Highscore: <span class="highscore">{highScore}</span>
		</p>
	</section>
</main>
