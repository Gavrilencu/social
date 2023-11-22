<script>
	// @ts-nocheck
	import { Card, Button, Label, Input, Checkbox } from 'flowbite-svelte';
	import { auth } from './store';
	import { change } from './store';
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';
	onMount(() => {
		auth.set('log');
	});

	let pass = null;
	let mail = null;
	async function Authentificate() {
		if (mail && pass) {
			let infoUsers = {
				email: mail,
				password: pass
			};
			const url = '/api/login';
			const response = await fetch(url, {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json'
				},

				body: JSON.stringify(infoUsers)
			});
			const data = await response.json();
			if (response.ok) {
				sessionStorage.setItem('username', data.username);
				auth.set('ok');
				goto('/home');
			} else {
				alert('Verificati datele');
			}
		} else {
			alert('Completati toate cimpurile');
		}
	}
</script>

<Card class="w-full max-w-md">
	<form class="flex flex-col space-y-6" action="/">
		<h3 class="text-xl font-medium text-gray-900 dark:text-white">Sign in to our platform</h3>
		<Label class="space-y-2">
			<span>Email</span>
			<Input type="text" name="email" bind:value={mail} placeholder="name@company.com" required />
		</Label>
		<Label class="space-y-2">
			<span>Your password</span>
			<Input type="password" name="password" bind:value={pass} placeholder="•••••" required />
		</Label>
		<div class="flex items-start">
			<Checkbox>Remember me</Checkbox>
			<a href="/" class="ml-auto text-sm text-primary-700 hover:underline dark:text-primary-500">
				Lost password?
			</a>
		</div>
		<Button type="submit" on:click={Authentificate} class="w-full">Login to your account</Button>
		<div class="text-sm font-medium text-gray-500 dark:text-gray-300">
			Not registered? <a
				href="/"
				on:click={() => {
					change.set('register');
				}}
				class="text-primary-700 hover:underline dark:text-primary-500"
			>
				Create account
			</a>
		</div>
	</form>
</Card>
