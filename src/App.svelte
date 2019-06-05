<script>
	let name = 'world';
	let st = '';
	let id = 0;
	let initialValue = {
		id: null,
		value: ''
	}
	let editing = {...initialValue};
	let tasks = [
		{
			id: 0,
			label: 'First your super puper task',
			value: 'First your super puper task'
		}
	];
	
	function addTask(e) {
		if (!st) return;
		const task = {
			id: id+=1,
			label: st,
			value: st
		};
		tasks = [...tasks, task];
		st = '';
}
	
	function deleteTask(id) {
		tasks = tasks.filter(t => t.id !== id);
	}
	
	function editTask(id, value) {
		editing.id = id;
		editing.value = value;
	}
	
	function saveTask() {
		console.log('save')
		tasks = tasks.map(task => {
			if (editing.id !== task.id) return task;
			return {...task, value: editing.value};
		});
		editing = {...initialValue};
	}

</script>

<style>	
	
	.todo {
		font-family: 'Dank Mono';
	}
	
	input {
		box-shadow: 8px 8px 8px -4px silver;
	}
	
	.btn {
		/*box-shadow: 8px 8px 8px -4px silver;*/
		outline: none;
		border: none;
		background: none;
		font-size: 18px;
	}
	
	.btn:active,input:focus {
		box-shadow: 5px 3px 10px -4px #0074D9;
	}
	
	.btn:focus {
		box-shadow: 6px 4px 8px -2px Navy, 5px 3px 10px -4px silver;
	}
	
	.delete,.edit {
		display: none;
		border: none;
		background-color: transparent;
		box-shadow: none;
		padding: 0;
		margin: 0;
	}
	
	li:hover .delete, li:hover .edit {
		display: inline-block;
	}
	
	li {
		margin-bottom: 5px;
	}
	
	li span {
		line-height: 35px;
	}
	
</style>

<div class='todo'> 
	<h1>Hello {name}!</h1>
<form on:submit|preventDefault={addTask} >
	<input placeholder='insert your value' bind:value={st} />
	<button class='btn' type='submit'>
		•
	</button>
</form>
<h2>
	Your super tasks:
</h2>
<ul>
	{#each tasks as task}
		<li>
			{#if editing.id === task.id}
				<input bind:value={editing.value} />
				<button class='delete' on:click={saveTask}>
					=
				</button>
			{:else}
				<span>{task.value}</span>
				<button class='delete' on:click={() => deleteTask(task.id)}>
					=
				</button>
				<button class='edit' on:click={() => editTask(task.id, task.value)}>
					=
				</button>
			{/if}
			
		</li>
	{/each}
</ul>
</div>






