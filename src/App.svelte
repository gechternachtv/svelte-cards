<script>
	import Card from './Card.svelte';
	import {allCards} from './Data.svelte';


	let filterOptions = (function(){
		const foo = [];
		allCards.forEach(card => card.tags.forEach(tag => foo.push(tag)))
		return new Set(foo);
	})()

	let activeFilters = [];

	
	$: activeCards = allCards.filter(card =>{
			if (activeFilters.length === 0){
				return true
			}else{
				return activeFilters.every(activeFilter => card.tags.includes(activeFilter))
			}
		})

	function filterClickHandler(){
		if(activeFilters.includes(this.value)){
			activeFilters = [...activeFilters].filter(value => value !== this.value)		
		}else{
			activeFilters = [...activeFilters, this.value];
		}
	}



</script>

<main>	
	
	<div class="filter" for="filter">

		{#each [...filterOptions] as filterOption}

			<button 
					on:click={filterClickHandler}
					class:active={activeFilters.includes(filterOption)} 
					value={filterOption}>
				{filterOption}
			</button>

		{/each}
	</div>

	<div class="card-container">

		{#each activeCards as card}
				<Card {...card}/>
		{/each}

	</div>
</main>

<style lang="scss">
	
	.filter{
		text-align: center;
		margin-bottom:20px;
	}

	.active {
		background-color: #ff3e00;
		color: white;
	}
	.card-container{
		display:grid;
		grid-template-columns:1fr 1fr 1fr;
		grid-gap:20px;
		max-width:1100px;
		margin:auto;
	}
</style>