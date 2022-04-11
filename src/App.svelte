<script>
	// calculator
	// components
	import Modal from './Modal.svelte';
	import Button from './Button/Button.svelte';
	import Screen from './Screen/Screen.svelte';
	import AddPersonForm from './AddPersonForm.svelte'
	const rows = [
		["7", "8", "9", "÷"],
		["4", "5", "6", "x"],
		["1", "2", "3", "-"],
		["0", "C", "=", "+"],
	];
	let result = "";

	// input, databinding
	let beltColor = "black";
	let firstName ="jimi";
	let lastName = "Hendrix";

	$: fullName = `${firstName} ${lastName}`;
	$: {
		console.log(beltColor);
		console.log(fullName);
	}


	const handleClick = () => {
		beltColor = "orange";
	}

	const handleInput = (e) => {
		beltColor = e.target.value;
	}

	// loops
	let people = [
		{name: 'yoshi', belColour: 'black', age: 25, id: 1},
		{name: 'mario', beltColour: 'orange', age: 45, id: 2},
		{name: 'luigi', beltColour: 'brown', age: 35, id: 3}
	]

	const handleDeletePerson = (id) => {
		// delete person from people
		// the filter() method creates a new array with all elements that pass the test implemented by the provided function
		people = people.filter((person) => person.id != id )
	}


	// conditionals
	let num = 3;

	// components, props
	let showModal = false;

	const toggleModal = () => {
		showModal = !showModal;
	}


</script>

{#if num > 20}
	<p>Greater than 20</p>
{:else if num > 5}
	<p>Greater than 5</p>
{:else}
	<p>Not greater than 5</p>
{/if}

<main>
	<h1>Máy tính</h1>
	<div class="keys">
		{#each rows as row}
		<div class="row">
			{#each row as key}
			<Button {key} bind:result />
			{/each}
		</div>
		{/each}
	</div>
	<Screen {result} />

	<h1>Input, Data binding</h1>
	<p style="color: {beltColor};">{fullName} - {beltColor} belt</p>
	<button on:click={handleClick}>update belt colour</button>
	<input type="text" bind:value={firstName}>
	<input type="text" bind:value={lastName}>
	<!-- <input type="text" on:input={handleInput} value={beltColor}> -->
	<input type="text" bind:value={beltColor}> <!--two-ways binding-->

	<h1>loops</h1>
	<div>
		{#each people as person (person.id)}
			<div>
				<h4>- {person.name}</h4>
				{#if person.belColour === 'black'}
					<p>MASTER NINJA</p>
				{/if}
				<p>{person.age} years old, {person.belColour} belt.</p>
				<button on:click={() => handleDeletePerson(person.id)}>delete</button>
			</div>
			{:else}
			<p>There are no people to show...</p>
		{/each}
	</div>

	<h1>Conditionals</h1>


	<!-- components -->
	<h1>Components, Props, Event Forwarding, Event Modifiers, Slot, Form</h1>
	<button on:click={toggleModal}>Open modal</button>
	<Modal message="Hey, i am a prop value" isPromo={true} {showModal} on:click={toggleModal}>
		<AddPersonForm />
		
	</Modal>



</main>

<style>
	main{
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	@media (min-width: 640px){
		main{
			max-width: none;
		}
	}

</style>