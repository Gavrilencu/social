<script>
	import '../app.css';
	import {
		Navbar,
		NavBrand,
		NavLi,
		NavUl,
		NavHamburger,
		Avatar,
		Dropdown,
		DropdownItem,
		DropdownHeader,
		DropdownDivider
	} from 'flowbite-svelte';
	import user from '$lib/img/user.png';
	import { auth } from '$lib/store';
	import { DarkMode } from 'flowbite-svelte';
	let darkmodebtn =
		'text-gray-500 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700 focus:outline-none focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-700 rounded-lg text-lg p-2.5 fixed right-4 top-2 z-50';
</script>

<DarkMode btnClass={darkmodebtn} />
{#if $auth !== 'log'}
	<Navbar>
		<NavBrand href="/home">
			<span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white"
				>Flowbite</span
			>
		</NavBrand>
		<div class="flex items-center md:order-2">
			<Avatar id="avatar-menu" class="avat" src={user} />
		</div>
		<Dropdown placement="bottom" triggeredBy="#avatar-menu">
			<DropdownHeader>
				<span class="block text-sm">{sessionStorage.getItem('username')}</span>
			</DropdownHeader>
			<DropdownItem>Profilul meu</DropdownItem>
			<DropdownItem>Setari</DropdownItem>
			<DropdownItem>Prieteni</DropdownItem>
			<DropdownDivider />
			<DropdownItem>Exit</DropdownItem>
		</Dropdown>
		<NavUl>
			<NavLi href="/home" active={true}>Home</NavLi>

			<NavLi href="">Message</NavLi>
		</NavUl>
	</Navbar>
{/if}
<slot />

<style>
	.flex {
		margin-right: 3rem;
	}
</style>
