<script>
  import Header from "$lib/Header.svelte";
  let tasks = [];
  //an array that will hold the list of tasks. ( Array starting point)

  function addTask() {
    //addTask is a function that adds a new empty string to the tasks array whenever it is called.(function annoucement/declaration)
    tasks = [...tasks, ""];
    //The function uses the spread syntax (...tasks) to create a new array that includes all existing tasks and adds an empty string at the end.
    //This new array overwrites the old one.
    //"" = a new item
  }
</script>

<Header />

<button on:click={addTask}>📝 Add</button>
<!-- attaches a click handler to the button that calls the addTask function. -->

{#each tasks as task, index}
  <!-- iterates over the tasks array, providing the task and its index. (returns value to the array) -->
  <div class="task">
    <input bind:value={tasks[index]} />
    <!-- binds the value of the input to the corresponding task in the tasks array, allowing for real-time updates. -->
  </div>
{/each}

<style>
  .task {
    display: block;
    /* each task input is displayed one below the other. */
  }
</style>
