<script>
	let enteredPw = '';
	let pwValidity = 'short';
	let passwords = [];

	$: if (enteredPw.trim().length < 5) {
		pwValidity = 'short';
	} else if (enteredPw.trim().length > 10) {
		pwValidity = 'long';
	} else {
		pwValidity = 'valid';
	}

	function confirmPw () {
		if (pwValidity === 'valid') {
			passwords = [...passwords, enteredPw];
		}
	}

	function removePw (index) {
		passwords = passwords.filter((pw, ind) => {
			return ind !== index;
		});
	}
</script>

<style>
input {
	width: 300px;
	margin-top: 20px;
	margin-bottom: 20px;
}
p {
	color: darkviolet;
}
.pw {
	color: #32CD32;
}
button {
	background-color: #F4A460;
	color: #fff;
	border-radius: 5px;
	padding: 10px;
}
</style>

<label for="password">Password</label>
<input type="password" bind:value={enteredPw} />
{#if pwValidity === 'short'}
	<p>Password be too short!</p>
{:else if pwValidity === 'long'}
	<p>Password be too Long!</p>
{:else}
	<p>Password: {enteredPw}</p>
{/if}
<button on:click="{confirmPw}">Add Password</button>
<!-- binding can be done 2 ways below -->
<ul>
	{#each passwords as pw, ind (pw)}
		<!-- <li class="pw" on:click="{removePw.bind(this, ind)}">{pw}</li> -->
		<li class="pw" on:click={() => removePw(ind)}>{pw}</li>
	{/each}
</ul>


<h1>Assignment</h1>

<p>Solve these tasks.</p>

<ol>
	<li>Add a password input field and save the user input in a variable.</li>
	<li>Output "Too short" if the password is shorter than 5 characters and "Too long" if it's longer than 10.</li>
	<li>Output the password in a paragraph tag if it's between these boundaries.</li>
	<li>Add a button and let the user add the passwords to an array.</li>
	<li>Output the array values (= passwords) in a unordered list (ul tag).</li>
	<li>Bonus: If a password is clicked, remove it from the list.</li>
</ol>
