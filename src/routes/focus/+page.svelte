<script lang="ts">
	import { Button, Dropdown } from 'stwui';

	let statusVisible = false;

	const toggleStatusDropdown = () => {
		statusVisible = !statusVisible;
	};

	const stati = [
		{
			label: 'To Do',
			value: 'todo',
			color: 'bg-blue-100 text-blue-600'
		},
		{
			label: 'In Progress',
			value: 'in-progress',
			color: 'bg-yellow-100 text-yellow-600'
		},
		{
			label: 'Done',
			value: 'done',
			color: 'bg-green-100 text-green-600'
		}
	];

	let currStatus = stati[0];
</script>

<Dropdown bind:visible={statusVisible}>
	<Button slot="trigger" type="danger" on:click={toggleStatusDropdown}>Done</Button>
	<Dropdown.Items slot="items">
		<form method="POST" action="?/changeStatus" class="gap-[4px] flex flex-col">
			<input type="hidden" name="status" bind:value={currStatus} />

			{#each stati as status}
				<Button
					type="danger"
					class="w-full justify-between {status.color}"
					on:click={() => (currStatus = status)}
				>
					{status.label}
				</Button>
			{/each}
		</form>
	</Dropdown.Items>
</Dropdown>
