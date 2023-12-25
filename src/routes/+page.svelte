<script lang="ts">
	import { tweened } from 'svelte/motion';
	import { tick } from 'svelte';

	let started = false;
	const codes = ['n4ughty', '3ric', 'isth3', 'b3st'];
	let guess1 = '';
	let guess2 = '';
	let guess3 = '';
	let guess4 = '';

	let original = 10 * 60; // TYPE NUMBER OF SECONDS HERE
	let timer = tweened(original);

	// ------ dont need to modify code below
	setInterval(() => {
		if (started && $timer > 0) $timer--;
	}, 1000);

	$: minutes = Math.floor($timer / 60);
	$: seconds = Math.floor($timer - minutes * 60);

	let currentStep = 0;

	const submitCode = (step, code) => {
		console.log(`submit ${step} ${code}`);
		if (codes[step - 1] === code) {
			currentStep++;
			scrollToStep(step);
		} else {
			alert('NOPE! Try again!');
		}
	};

	const scrollToStep = async (step) => {
		await tick();
		const el = document.querySelector(`#step-${step}`);
		console.log(el);
		el?.scrollIntoView({ behavior: 'smooth' });
	};
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Naughty Eric" />
</svelte:head>

<section>
	<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Flat_Eric_pose_2.jpg" />
	<h1>GUESS WHOOOO!!!</h1>

	<p>
		Hello Reuben and Phoenix - isn't this a surprise!<br />
		I've done it <i>again</i>, as I'm sure you've surmised:<br />
		I've <strong>taken the prezzies!</strong> I've <strong>hid them away!</strong><br />
		And I reckon I'll get a fair bit on eBay...
	</p>
	<p>
		<i>BUT</i> as you know by now, I love a good game<br />
		So if you can find me (which <i>would</i> be a shame)<br />
		Then I'll give you them back and we'll call it a draw<br />
		But can you do it in time? I'm not so sure...
	</p>
	<p>
		You've got <i>10 whole minutes</i> to follow these clues<br />
		Before I do what the Grinch <i>almost</i> did to those <i>Who</i>s!<br />
		Simply enter each code to unlock the next clue<br />
		Are you ready? Then let's do it - <b>I'm waiting for you!</b>
	</p>

	<span>{minutes.toString().padStart(2, '0')}:{seconds.toString().padStart(2, '0')}</span>
	<progress value={$timer / original} />
	<br />

	<button
		class={currentStep > 0 ? 'disabled' : ''}
		disabled={currentStep > 0}
		on:click={() => {
			currentStep = 1;
			started = true;
			scrollToStep(1);
		}}>BEGIN</button
	>

	{#if currentStep > 0}
		<div id="step-1" class="step">
			<p>
				The first clue could be slightly mean<br />
				For people who are never clean<br />
				Sometimes it rains, sometimes it pours<br />
				But what thing makes that happen indoors?
			</p>
			<form on:submit|preventDefault={() => submitCode(1, guess1)}>
				<label for="clue-1">CODE:</label>
				<input id="clue-1" type="text" bind:value={guess1} autocomplete="off" />
				<button
					class={`submit ${currentStep > 1 ? 'disabled' : ''}`}
					type="submit"
					disabled={currentStep > 1}>SUBMIT</button
				>
				{#if currentStep > 1}
					<div style="width: 20px">
						<img
							src="https://upload.wikimedia.org/wikipedia/commons/8/8b/Eo_circle_green_white_checkmark.svg"
						/>
					</div>
				{/if}
			</form>
		</div>
	{/if}
	{#if currentStep > 1}
		<div id="step-2" class="step">
			<p>
				The oats and the carrots should all be gone<br />
				A festive treat to be fed upon<br />
				That’s all well and good for <i>Santa’s</i> reindeer<br />
				But isn't there one who already lives here?
			</p>
			<form on:submit|preventDefault={() => submitCode(2, guess2)}>
				<label for="clue-2">CODE:</label>
				<input id="clue-2" type="text" bind:value={guess2} autocomplete="off" />
				<button
					class={`submit ${currentStep > 2 ? 'disabled' : ''}`}
					type="submit"
					disabled={currentStep > 2}>SUBMIT</button
				>
				{#if currentStep > 2}
					<div style="width: 20px">
						<img
							src="https://upload.wikimedia.org/wikipedia/commons/8/8b/Eo_circle_green_white_checkmark.svg"
						/>
					</div>
				{/if}
			</form>
		</div>
	{/if}
	{#if currentStep > 2}
		<div id="step-3" class="step">
			<p>
				By now Phoen’s probably had enough<br />
				And all I’ll say to that is: tough!<br />
				Finding this code will prove his worth<br />
				It’s on a picture from his birth!
			</p>
			<form on:submit|preventDefault={() => submitCode(3, guess3)}>
				<label for="clue-3">CODE:</label>
				<input id="clue-3" type="text" bind:value={guess3} autocomplete="off" />
				<button
					class={`submit ${currentStep > 3 ? 'disabled' : ''}`}
					type="submit"
					disabled={currentStep > 3}>SUBMIT</button
				>
				{#if currentStep > 3}
					<div style="width: 20px">
						<img
							src="https://upload.wikimedia.org/wikipedia/commons/8/8b/Eo_circle_green_white_checkmark.svg"
						/>
					</div>
				{/if}
			</form>
		</div>
	{/if}
	{#if currentStep > 3}
		<div id="step-4" class="step">
			<p>
				I can’t believe you’ve made it here<br />
				But this one is too hard, I fear<br />
				It might just catch you unawares<br />
				You hold this to go up the stairs
			</p>
			<form on:submit|preventDefault={() => submitCode(4, guess4)}>
				<label for="clue-4">CODE:</label>
				<input id="clue-4" type="text" bind:value={guess4} autocomplete="off" />
				<button
					class={`submit ${currentStep > 4 ? 'disabled' : ''}`}
					type="submit"
					disabled={currentStep > 4}>SUBMIT</button
				>
				{#if currentStep > 4}
					<div style="width: 20px">
						<img
							src="https://upload.wikimedia.org/wikipedia/commons/8/8b/Eo_circle_green_white_checkmark.svg"
						/>
					</div>
				{/if}
			</form>
		</div>
	{/if}
	{#if currentStep > 4}
		<div id="step-5" class="step">
			<p>
				These presents are about to meet their doom...<br />
				<strong>UNLESS YOU RUN DOWN TO THE GARDEN ROOM!!</strong>
			</p>
		</div>
	{/if}
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	p {
		width: 50%;
	}

	button {
		background-color: #be0b00;
		color: #fff;
		font-weight: bold;
		text-transform: uppercase;
		outline: 0;
		border: none;
		border-radius: 6px;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.199);
		transition: box-shadow scale 100ms ease-in;
		cursor: pointer;
		font-size: 2rem;
	}

	.disabled {
		background-color: #808080;
	}

	.submit {
		font-size: 1.5rem;
	}

	form {
		display: flex;
		align-items: center;
		gap: 20px;
	}

	.step {
		width: 50%;
		margin: auto;
	}

	.step > p {
		width: 100%;
	}
</style>
