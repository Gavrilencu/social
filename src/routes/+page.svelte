<script>
	import Login from '$lib/Login.svelte';
	import Register from '$lib/Register.svelte';
	import { change } from '$lib/store';
</script>

<div class="app">
	{#if $change === 'login'}
		<Login />
	{:else if $change === 'register'}
		<Register />
	{/if}
</div>

<style>
	.app {
		width: 100%;
		height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>
