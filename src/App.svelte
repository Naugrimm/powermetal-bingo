<script>
	import { toSvg, toPng } from "html-to-image";
	import download from "downloadjs";

	// Body
	let backgroundCls = "bg-black";
	let fontFamily = "Metal Mania";
	let textSizeCls = "text-9xl";
	
	// Header
	let header = "Powermetal Bingo";
	let headerCls = "text-16xl py-12";
	
	// Grid
	let columns = 5;
	let rows = 5;
	let textColorCls = "text-gray-200";
	let border = "border-2 border-gray-200";
	let paddingY = "py-20";
	let mustHave = [
			"beer",
			"pirate",
			"mighty",
			"metal",
			"steel",
	];
	
	let words = [
		"ancient",
		"angel",
		"arms",
		"army",
		"ashes",
		"axe",
		"babylon",
		"battle",
		"beer",
		"bloody",
		"born",
		"burning",
		"chaos",
		"damned",
		"darkness",
		"dawn",
		"demons",
		"draconian",
		"dreams",
		"dying",
		"endless",
		"eternity",
		"evil",
		"eyes",
		"fallen",
		"fantasy",
		"fate",
		"flames",
		"forever",
		"freedom",
		"future",
		"galaxy",
		"glory",
		"gold",
		"hammer",
		"hearts",
		"heaven",
		"heroes",
		"holy",
		"kingdom",
		"magic",
		"magnetic",
		"march",
		"metal",
		"mighty",
		"north",
		"paradise",
		"pirate",
		"rage",
		"riding",
		"rise",
		"rule",
		"rum",
		"seas",
		"shadows",
		"shield",
		"shore",
		"skies",
		"souls",
		"steel",
		"sword",
		"tears",
		"things",
		"thunder",
		"universe",
		"warrior",
	];
	// console.log(JSON.stringify(words.filter((v, i, a) => a.indexOf(v) === i).sort(), null, 2));
	let sliced = words
		.sort(() => Math.random() - 0.5)
		.slice(0, rows * columns);

	let finalWords = mustHave;
	let iterations = 0;
	let maxIterations = words.length;
	do {
		let word = words[Math.floor(Math.random() * maxIterations)];
		if (finalWords.indexOf(word) === -1) {
			finalWords.push(word);
		}
		iterations++;
	} while (finalWords.length < rows * columns && iterations < maxIterations)

	finalWords.sort(() => Math.random() - 0.5);

	const downloadSvg = (event) => {
		document.getElementById('container').classList.remove(backgroundCls);
		toPng(document.getElementById('container'), { width: 2800, height: 2500  })
				.then(function (dataUrl) {
					download(dataUrl, "powermetal-bingo.png");

					document.getElementById('container').classList.add(backgroundCls);
				});
	}
</script>
<svelte:head>
	<link href="https://unpkg.com/tailwindcss@^2.0/dist/tailwind.min.css" rel="stylesheet"/>
</svelte:head>

<style>
	.text-16xl {
		font-size: 16rem;
	}
</style>

<body class="{textColorCls} {textSizeCls}" style="font-family: {fontFamily};">
	<div id="container" class="{backgroundCls}">
		<div class="grid grid-cols-1">
			<div class="text-center {headerCls}" on:click={downloadSvg}>
				<h1>
					{header}
				</h1>
			</div>
		</div>
		<div class="grid grid-cols-{columns} ring-2 ring-gray-200">
			{#each finalWords as word}
				<div class="word {border} {paddingY} text-center">{word.charAt(0).toUpperCase() + word.slice(1)}</div>
			{/each}
		</div>
	</div>
</body>
