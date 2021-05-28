<script>
	import ContactCard from './ContactCard.svelte';

	let name = 'Donghee';
	let title = '';
	let image = '';
	let description = '';
	let age = 33;

	// 따로 선언 안해줘도 됨
	$: uppercaseName = name.toUpperCase();

	$: console.log(name);

	// 이름이 DongDonghee 일 경우 실행
	$: if (name === 'DongDonghee') {
		console.log('It runs!')
		age = 34;
	}

	function incrementAge() {
		age += 1;
	}

	function changeName() {
		name = 'DongDonghee';
	}

	function nameInput(event) {
		const enteredValue = event.target.value;
		name = enteredValue;
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {uppercaseName}, my age is {age}!</h1>
<button on:click={incrementAge}>Change Age</button>
<button on:click={changeName}>Change Name</button>
<!-- 단방향 -->
<input type="text" value={name} on:input={nameInput}>
<!-- 양방향 -->
<input type="text" bind:value={name}>
<input type="text" bind:value={title}>
<input type="text" bind:value={image}>
<textarea rows="3" bind:value={description}></textarea>
<ContactCard userName={name} userImage={image} jobTitle={title} {description}/>