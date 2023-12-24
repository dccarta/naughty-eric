<script>
	import { tweened } from 'svelte/motion';

	let original = 10 * 60; // TYPE NUMBER OF SECONDS HERE
	let timer = tweened(original);

	// ------ dont need to modify code below
	setInterval(() => {
		if ($timer > 0) $timer--;
	}, 1000);

	$: minutes = Math.floor($timer / 60);
	$: seconds = Math.floor($timer - minutes * 60);
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Naughty Eric" />
</svelte:head>

<section>
	<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Flat_Eric_pose_2.jpg" />
	<h1>GUESS WHOOOO!!!</h1>

	<span>{minutes.toString().padStart(2, '0')}:{seconds.toString().padStart(2, '0')}</span>
	<progress value={$timer / original} />

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
	<button class="">BEGIN</button>
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
		--primary: #be0b00;
		--primary-text: #fff;
		--secondary: #775655;
		--secondary-text: #fff;
		--neutral: #f4dddc;
		--neutral-text: #524342;
		--focus-ring: #857372;
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
</style>
