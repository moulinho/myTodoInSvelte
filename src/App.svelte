<script>
	import { fade } from 'svelte/transition';
  let tasks = [
    {
      name: "Task",
      complete: false,
    },
  ];

  let newTasks = "";

  let addTask = () => {
    tasks = [
      ...tasks,
      {
        id: Date.now(),
        name: newTasks,
        complete: false,
      },
    ];
    newTasks = "";
  };

  let deleteTask = (id) => {
    tasks = [...tasks.filter((t) => t.id != id)];
  };
</script>

<main>
  <h3>MyTodo </h3>
  <ul>
    {#each tasks as task (task.id)}
      <li transition:fade >
        <input type="checkbox" bind:checked={task.complete} />
        <span class:checked={task.complete}>{task.name}</span>
        <button on:click={deleteTask(task.id)}>X</button>
      </li>
    {/each}
  </ul>
  <input type="text" name="" id="" bind:value={newTasks} />
  <button on:click|preventDefault={addTask}> add task</button>
  {JSON.stringify(tasks)}
</main>

<style>
  .checked {
    text-decoration: line-through;
  }
</style>
