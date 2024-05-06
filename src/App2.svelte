<script>
  import { onMount } from "svelte";

	import CardList from "./Cards.svelte";
	import Card from "./lib/components/CardProxy.svelte";

	let basicGallery;

	let query = "";
	let isLoading = true;

	function zoneCards() {

		let cards = [];
		for (let i = 1; i <= 24; i++) {
			let type = "character";
			cards.push({
				"id": "swsh11tg-TG05",
				"set": "swsh11tg",
				"name": "Pikachu",
				"supertype": "Pokémon",
				"subtypes": ["Basic"],
				"types": ["Lightning"],
				"number": "TG05",
				"count": `${i}`,
				"rarity": "trainer gallery rare holo",
				"images": {
					"small": `./zonecards/${type}_front_${i} .${i}.png`,
					"large": `./zonecards/${type}_front_${i} .${i}.png`,
					"foil": `../../zonecards/alpha/inverted/inverted_${type}_holo_${i}%20.${i}.png`,
					"mask": `../../zonecards/alpha/inverted/inverted_${type}_holo_${i}%20.${i}.png`,
				}
			});
		}
		for (let i = 1; i <= 6; i++) {
			let type = "test";
			cards.push({
				"id": "swsh11tg-TG05",
				"set": "swsh11tg",
				"name": "Pikachu",
				"supertype": "Pokémon",
				"subtypes": ["Basic"],
				"types": ["Lightning"],
				"number": "TG05",
				"count": `${i}`,
				"rarity": "trainer gallery rare holo",
				"images": {
					"small": `./zonecards/${type}_front_${i} .${i}.png`,
					"large": `./zonecards/${type}_front_${i} .${i}.png`,
					"foil": `../../zonecards/alpha/inverted/inverted_${type}_holo_${i}%20.${i}.png`,
					"mask": `../../zonecards/alpha/inverted/inverted_${type}_holo_${i}%20.${i}.png`,
				}
			});
		}		
		return cards;
	}


	const loadCards = async() => {
		window.cards = zoneCards();
		basicGallery = zoneCards();
		isLoading = false;
	};


	onMount(() => {
		loadCards();
		const $headings = document.querySelectorAll("h1,h2,h3");
		const $anchor = [...$headings].filter((el) => {
			const id = el.getAttribute("id")?.replace(/^.*?-/g,"");
			const hash = window.location.hash?.replace(/^.*?-/g,"")
			return id === hash;
		})[0];
		if( $anchor ) {
			setTimeout(() => {
				$anchor.scrollIntoView();
			},100);
		}
	});
</script>

<main>


	{#if query.length < 3}

		<CardList>
			{#if isLoading}
				loading...
			{:else}
				{#each basicGallery as card, index}
					<Card
						id={card.id}
						name={card.name}
						number={card.number}
						count={card.count}
						set={card.set}
						types={card.types}
						supertype={card.supertype}
						subtypes={card.subtypes}
						rarity={card.rarity}
						img={card.images.small}
						foil={card.images.foil}
						mask={card.images.mask}
					/>
				{/each}
			{/if}
		</CardList>

	{/if}
</main>

<div class="back-to-top">
  <a href="#⚓-top">Back to Top</a>
</div>

<style>
  .back-to-top a {
    color: inherit;
    text-decoration: none;
		z-index: 999;
  }
</style>
