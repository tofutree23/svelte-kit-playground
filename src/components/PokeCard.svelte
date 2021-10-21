<script lang="ts">
	import Card, { Media, MediaContent, Content } from '@smui/card'

	export let handleClickPokemon: (id: number) => void
	export let id: number
	export let image: string
	export let name: string
</script>

<svelte:head>
	<style lang="scss">
		.card-temp {
			background: lightblue;
		}
		.pokecard-media-content {
			display: flex;
			justify-content: center;
		}
		.pokecard-content {
			display: flex;
			justify-content: center;
		}
	</style>
</svelte:head>

<Card class="card-temp" variant="raised" on:click={() => handleClickPokemon(id)}>
	<Media aspectRatio="16x9">
		<MediaContent class="pokecard-media-content">
			<img src={image} alt={name} />
		</MediaContent>
	</Media>
	<Content class="pokecard-content">#{id} {name.toUpperCase()}</Content>
</Card>
