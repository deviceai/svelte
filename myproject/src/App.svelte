<script>
	import Modal from "./Modal.svelte";
	import AddPersonForm from "./AddPersonForm.svelte";

	let firstName = 'Alex';
	let lastName = 'Smith'
	let beltcolor = 'blue';

	let people = [
		{name: 'Alex', beltcolor: 'black', age: 25, id: 1},
		{name: 'Tom', beltcolor: 'red', age: 15, id: 2},
		{name: 'John', beltcolor: 'blue', age: 38, id: 3}
	];

	let num = 5;

	let showModal = false;
	let showAddPersonForm = false;

	// Reactive value, automaticaly updates
	$: fullName = `${firstName} ${lastName}`;
	// $: console.log(beltcolor);
	$: {
		console.log(firstName);
		console.log(lastName);
	};
	const handleClick = () => {
		beltcolor = 'orange';
	};
	const handleInput = (e) => {
		beltcolor = e.target.value;
	};
	const deletePerson = (id) => {
		//delete person form people
		// console.log(id);
		people = people.filter((person) => person.id != id );
	};
	const openModal = () => {
		showModal = !showModal;
	};
	const openAddPersonForm = () => {
		showAddPersonForm = !showAddPersonForm;
	};
	const addPerson = (e) => {
		console.log("addPerson:")
		console.log(e.detail)

		const person = e.detail;
		people = [person, ...people];
		showAddPersonForm = false;
	};
</script>

<Modal message="Hey, I am a prop value" isPromo={true} showModal={showModal} on:click={openModal}/>
<AddPersonForm {showAddPersonForm} on:click={openAddPersonForm} on:addPerson={addPerson}/>

<Modal {showModal} on:click={openModal}>
	<div slot="title">
		<h3>Add new person</h3>
	</div>
<form>
	<input type="text" placeholder="name">
	<input type="text" placeholder="belt color">
	<button>Add person</button>
</form>
</Modal>

<main>
	<h1>Hello {firstName} {lastName}!</h1>
	<p style="color: {beltcolor}">{fullName}, color is {beltcolor}</p>
	<button on:click={handleClick}>update color</button>
	<!-- <input type="text" on:input={handleInput} value={beltcolor}> -->
	<input type = "text" bind:value={beltcolor}>

	<p></p>
	<input type="text" bind:value={firstName}>
	<input type="text" bind:value={lastName}>

	<div>
		<!-- <h4>{people[0].name}</h4>
		<p>{people[0].beltcolor}</p> -->
		<p></p>
		<h4>Persons:</h4>
		{#each people as person}
	<div>
		<p>{person.name} is {person.age} years old, and his/her color is {person.beltcolor}</p>
		<button on:click={() => deletePerson(person.id)}>delete</button>
	</div>
		{:else}
		<p>There is no people to show...</p>
		{/each}
	</div>

	<div>
		{#if num > 20}
			<p>Greater than 20</p>
		{:else if num >= 5}
			<p>Greater than 5</p>
		{:else}
			<p>Lower that 5</p>
		{/if}
	</div>


	<div>
		<p>Show Promo</p>
		<button on:click|once={openModal}>Open</button>
	</div>

	<div>
		<p>Add person</p>
		<button on:click={openAddPersonForm}>Add</button>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>