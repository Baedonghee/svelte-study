<script>
	import CustomInput from './CustomInput.svelte';
	import Toggle from './Toggle.svelte';
	import { isValidEmail } from './validation';

	let val = 'Dong';
	let price = 0;
	let selectedOption = 1;
	let agreed;
	let favColor = 'red';
	let favColorCheckBox = ['red'];
	let singleFavColor = 'red';
	let usernameInput;
	let someDiv;
	let customInput;
	let enteredEmail = '';
	let formIsValid = false;

	$: if (isValidEmail(enteredEmail)) {
		formIsValid = true;
	} else {
		formIsValid = false;
	}

	function saveData() {
		console.log(usernameInput.value);
		console.dir(someDiv);
		// console.log(document.querySelector('#username').value);
		customInput.empty();
	}
</script>

<style>
	.invalid {
		border: 1px solid red;
	}
</style>



<CustomInput bind:val={val} bind:this={customInput}/>
<!-- <input type="text" bind:value={val} /> -->

<Toggle bind:chosenOption={selectedOption} />

<input type="number" bind:value={price} />

<label>
	<input type="checkbox" bind:checked={agreed} />
	Agree to terms?
</label>

<h1>Favorite Color?</h1>
<label>
	<input type="radio" name="color" value="red" bind:group={favColor} />
	Red
</label>
<label>
	<input type="radio" name="color" value="green" bind:group={favColor}/>
	Green
</label>
<label>
	<input type="radio" name="color" value="blue" bind:group={favColor}/>
	Blue
</label>

<h1>Favorite Color?</h1>
<label>
	<input type="checkbox" name="color" value="red" bind:group={favColorCheckBox} />
	Red
</label>
<label>
	<input type="checkbox" name="color" value="green" bind:group={favColorCheckBox}/>
	Green
</label>
<label>
	<input type="checkbox" name="color" value="blue" bind:group={favColorCheckBox}/>
	Blue
</label>

<select bind:value={singleFavColor}>
	<option value="green">Green</option>
	<option value="red">Red</option>
	<option value="blue">Blue</option>
</select>

<input type="text" id="username" bind:this={usernameInput} />
<button on:click={saveData}>Save</button>

<div bind:this={someDiv}></div>

<hr>

<form on:submit|preventDefault>
	<input type="email" bind:value={enteredEmail} class={isValidEmail(enteredEmail) ? '' : 'invalid'}/>
	<button type="submit" disabled={!formIsValid}>Save</button>
</form>