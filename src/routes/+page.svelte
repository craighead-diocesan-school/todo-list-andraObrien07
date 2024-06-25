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
  function removeTask(index) {
    const firstPart = tasks.slice(0, index);
    //creates a new array that includes all elements from the start of the tasks array up to (but not including) the element at index.

    const secondPart = tasks.slice(index + 1);
    //creates a new array that includes all elements from the element immediately after index to the end of the tasks array.

    tasks = [...firstPart, ...secondPart];
    //(...) is used to concatenate these two arrays, basically creating a new array out of the old one, but leaving out the element at index.
  }

  function saveTasks() {
    const tasksAsJSON = JSON.stringify(tasks);
    //The tasks array, which is a JavaScript object, is converted to a JSON string. Converting the tasks array to a JSON string is necessary because localStorage can only store strings.
    localStorage.todos = tasksAsJSON;
    //local storage is an API that allows you to store key-value pairs in a web browser. Data stored in localStorage has no expiration time, meaning it will stay until it's deleted.
    //The JSON string representation of the tasks array is stored in localStorage under the key todos. This means that the tasks array is saved as a string in the browser's local storage and can be retrieved later.
  }

  function loadTasks() {
    const tasksAsJSON = localStorage.todos;
    // localStorage.todos: This gets the value stored in localStorage under the key todos. This is the JSON string that was previously saved by the saveTasks function.
    const tasksAsArray = JSON.parse(tasksAsJSON);
    // The JSON.parse function converts the JSON string back into the array of tasks.

    tasks = tasksAsArray;
    // This overwrites the tasks array with the tasks that were previously saved.
  }
</script>

<Header />

<button on:click={addTask}>📝 Add</button>
<!-- attaches a click handler to the button that calls the addTask function. -->

<button on:click={saveTasks}> 💾 save</button>
<!-- <button
  on:click={() => {
    saveTasks(index);
  }}>💾 save</button
> -->

<button on:click={loadTasks}> 📡 load</button>
<!-- <button
  on:click={() => {
    loadTasks(index);
  }}>📡 load</button
> -->

{#each tasks as task, index}
  <!-- iterates over the tasks array, providing the task and its index. (returns value to the array) -->

  <div class="inputRemove">
    <div class="task">
      <input bind:value={tasks[index]} />
      <!-- binds the value of the input to the corresponding task in the tasks array, allowing for real-time updates. -->
    </div>

    <button
      on:click={() => {
        removeTask(index);
      }}>🗑 remove</button
    >
  </div>
{/each}

<style>
  .task {
    display: block;
    /* each task input is displayed one below the other. */
  }

  .inputRemove {
    display: flex;
    align-items: center;
    /* puts the input box and the remove icon next to eachother */
  }
</style>
