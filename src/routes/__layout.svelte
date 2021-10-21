<script lang="ts">
	import Nav from '../components/Nav.svelte'
</script>

<Nav />
<div>
	<slot />
	<footer>{new Date().getFullYear()}</footer>
</div>

<style lang="scss">
	div {
		position: relative;
		padding: 2rem;
		top: 50px;
		height: calc(100vh - 50px - 2rem);
		overflow: auto;
	}

	footer {
		position: absolute;
		display: flex;
		justify-content: center;
		align-items: center;
		width: 100%;
		bottom: 15px;
	}
</style>
