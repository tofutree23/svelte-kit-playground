<script lang="ts">
	import Card from '@smui/card'
	import Dialog, { Title, Content, Actions } from '@smui/dialog'
	import Button from '@smui/button'

	let open = false
</script>

<svelte:head>
	<title>About</title>
</svelte:head>

<div>
	<Dialog bind:open>
		<Title>Dialog</Title>
		<Content>This is dialog</Content>
		<Actions>
			<Button>Confirm</Button>
			<Button>Close</Button>
		</Actions>
	</Dialog>
	<Button variant="raised" on:click={() => (open = true)}>open dialog</Button>
</div>

<style lang="scss">
	div {
		display: flex;
	}
</style>
