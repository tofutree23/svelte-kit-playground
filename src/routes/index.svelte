<script lang="ts">
	import { onMount } from 'svelte'
	import Dialog, { Title, Content, Actions } from '@smui/dialog'
	import Textfield from '@smui/textfield'
	import LinearProgress from '@smui/linear-progress'
	import CircularProgress from '@smui/circular-progress'
	import Button from '@smui/button'

	import { pokemons, fetchPokemon } from '../stores/rootStore'
	import PokeCard from '../components/PokeCard.svelte'

	// states
	let filteredPokemons: any[] = [...$pokemons]
	let selectedPokemonInfo: any
	let dialogOpen: boolean = false
	let searchText: string = ''
	let isLoaded: boolean = false

	// onMount
	onMount(async () => {
		isLoaded = false
		try {
			await fetchPokemon()
			isLoaded = true
		} catch (error) {
			console.error('fail to fetch pokemons')
		}
	})

	// handler
	async function handleClickPokemon(id: number) {
		dialogOpen = true

		const url = `https://pokeapi.co/api/v2/pokemon/${id}`
		const res = await fetch(url)
		const pokemon = await res.json()
		selectedPokemonInfo = {
			...pokemon,
			image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/home/${id}.png`,
		}

		console.log(selectedPokemonInfo, 'SELECTED')
	}

	// effects
	$: {
		if (searchText) {
			filteredPokemons = $pokemons.filter((pokemon) =>
				pokemon.name.includes(searchText.toLocaleLowerCase())
			)
		} else {
			filteredPokemons = [...$pokemons]
		}

		if (!dialogOpen) {
			selectedPokemonInfo = undefined
		}
	}
</script>

<svelte:head>
	<title>PokeDex</title>
	<style lang="scss">
		.index-textfield {
			width: 100%;
			margin-bottom: 20px;
		}
	</style>
</svelte:head>

<Textfield
	class="index-textfield"
	label="Search your pokemon"
	variant="outlined"
	bind:value={searchText}
/>

{#if isLoaded}
	<div class="pokemons">
		{#each filteredPokemons as pokemon}
			<PokeCard {handleClickPokemon} id={pokemon.id} name={pokemon.name} image={pokemon.image} />
		{/each}
	</div>
{:else}
	<LinearProgress indeterminate closed={isLoaded} />
{/if}

<Dialog
	bind:open={dialogOpen}
	scrimClickAction=""
	escapeKeyAction=""
	aria-labelledby="list-title"
	aria-describedby="list-content"
	surface$style="width: 850px; max-width: calc(100vw - 32px); height: 50rem; max-height: calc(100vh - 32px)"
>
	<Title id="list-title">
		{#if selectedPokemonInfo}
			{selectedPokemonInfo.name.toLocaleUpperCase()}
		{:else}
			<CircularProgress style="height: 32px; width: 32px;" indeterminate />
		{/if}
	</Title>
	<Content id="list-content">
		{#if selectedPokemonInfo}
			<div class="index-dialog-img-section">
				<img src={selectedPokemonInfo?.image} alt={selectedPokemonInfo?.name} />
			</div>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
			<p class="mdc-typography--button">hehehe</p>
		{:else}
			<CircularProgress style="height: 32px; width: 32px;" indeterminate />
		{/if}
	</Content>
	<Actions>
		<Button>close</Button>
	</Actions>
</Dialog>

<style lang="scss">
	.pokemons {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		row-gap: 10px;
		column-gap: 10px;
	}

	.index-dialog-img-section {
		display: flex;
		justify-content: center;
	}
</style>
