<script>
	let uid = 0;
	let newTask = '';
	let tasks = [];

	function add() {
		// split task & tags
		const tagRegex = /@(\S+)/g;
		const matches = newTask.match(tagRegex) || [];
		const tags = new Set(matches.map((tag) => tag.slice(1)));
		const task = newTask.replace(tagRegex, '').trim();

		tasks = [{ id: uid++, task: task, tags: Array.from(tags) }, ...tasks];
		newTask = '';
	}
</script>

<main class="bg-gray-100 min-h-screen flex flex-col justify-center items-center p-4">
	<h1 class="text-4xl font-semibold mb-4">Dots: Todo for minimalists.</h1>

	<label for="newTask" class="text-lg mb-2">New Todo Item:</label>

	<input
		id="newTask"
		type="text"
		bind:value={newTask}
		on:keydown={(e) => e.key === 'Enter' && add()}
		maxlength="60"
		placeholder="Enter a new todo item..."
		class="bg-gray-200 text-gray-800 px-4 py-2 rounded-md shadow-md focus:outline-none focus:ring focus:border-blue-300"
	/>

	<section class="mt-4 space-y-4">
		{#each tasks as task (task.id)}
			<div class="bg-white p-4 rounded-lg shadow-md">
				<p class="text-lg font-semibold">{task.task}</p>
				<ul class="mt-2 space-x-2">
					{#each task.tags as tag (tag)}
						<li class="inline-block bg-gray-200 text-gray-800 px-2 py-1 rounded-md">{tag}</li>
					{/each}
				</ul>
			</div>
		{/each}
	</section>
</main>
