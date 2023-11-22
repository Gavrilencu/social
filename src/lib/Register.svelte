<script>
	// @ts-nocheck
	import { Card, Button, Label, Input, Checkbox } from 'flowbite-svelte';
	import { change } from './store';
	import { goto } from '$app/navigation';
	import { auth } from './store';
	import { onMount } from 'svelte';
	onMount(() => {
		auth.set('log');
	});
	let name = null;
	let pass = null;
	let pass2 = null;
	let mail = null;
	async function RegisterUsers() {
		if (name && pass === pass2 && mail) {
			let infoUsers = {
				username: name,
				email: mail,
				password: pass
			};
			const url = '/api/register';
			const response = await fetch(url, {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json'
				},

				body: JSON.stringify(infoUsers)
			});
			const data = await response.json();
			if (response.ok) {
				sessionStorage.setItem('username', name);
				auth.set('ok');
				goto('/home');
			}
		} else {
			alert('Complectati toate cimpurile*');
		}
	}
</script>

<Card class="w-full max-w-md">
	<form class="flex flex-col space-y-6" action="/">
		<h3 class="text-xl font-medium text-gray-900 dark:text-white">Register</h3>
		<Label class="space-y-2">
			<span>Email</span>
			<Input type="text" name="email" bind:value={mail} placeholder="name@company.com" required />
		</Label>
		<Label class="space-y-2">
			<span>Name Surname</span>
			<Input type="text" name="email" bind:value={name} placeholder="John Doe" required />
		</Label>
		<Label class="space-y-2">
			<span>Password</span>
			<Input type="password" name="password" bind:value={pass} placeholder="•••••" required />
		</Label>
		<Label class="space-y-2">
			<span>Repeat password</span>
			<Input type="password" name="password" bind:value={pass2} placeholder="•••••" required />
		</Label>
		<div class="flex items-start">
			<Checkbox>Remember me</Checkbox>
			<a href="/" class="ml-auto text-sm text-primary-700 hover:underline dark:text-primary-500">
				Lost password?
			</a>
		</div>
		<Button type="submit" on:click={RegisterUsers} class="w-full">Register your account</Button>
		<div class="text-sm font-medium text-gray-500 dark:text-gray-300">
			Have a acount? <a
				href="/"
				on:click={() => {
					change.set('login');
				}}
				class="text-primary-700 hover:underline dark:text-primary-500"
			>
				Login
			</a>
		</div>
	</form>
</Card>
