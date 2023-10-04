<script>	
	import Header from "./components/Header.svelte";
	import Footer from "./components/Footer.svelte";
	import Tabs from "./shared/Tabs.svelte";

	//TABS
	let items = ['Current Polls', 'Add new poll'];
	let activeItem = 'Current Polls';

	const tabChange = (e) => {
		activeItem = e.detail;
	}
</script>

<Header />

<main>
	<Tabs {activeItem} {items} on:tabChange={tabChange}/>
	{#if activeItem === 'Current Polls'}
		<p>Poll list component goes here</p>
	{:else if activeItem = 'Add new poll'}
		<p>New poll component goes here</p>
	{/if}
</main>

<Footer />

<style>
	main{
		max-width: 960px;
		margin: 40px auto;
	}

</style>ß