<script>
  import { onMount } from "svelte";

  let tasks = [];
  tasks = window.localStorage.getItem("Tasks");

  if (tasks) {
    tasks = JSON.parse(tasks);
  }

  let text = "";

  function addTask() {
    let updatedTasks = tasks;

    function constructDate() {
      let now = new Date();
      return now.getMonth() + "/" + now.getDate() + "/" + now.getFullYear();
    }

    const newTask = {
      text: text,
      date: constructDate(),
    };

    if (updatedTasks) {
      updatedTasks.push(newTask);
    } else {
      updatedTasks = [newTask];
    }

    window.localStorage.setItem("Tasks", JSON.stringify(updatedTasks));
    tasks = JSON.parse(window.localStorage.getItem("Tasks"));
    text = "";
  }
</script>

<style>
  section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 40rem;
  }

  input {
    width: 80%;
  }
</style>

<section>
  <div>
    <input bind:value={text} placeholder="Enter a task to complete" />
    <button on:click={addTask}>Add</button>
  </div>
  <div>
    {#if tasks}
      {#each tasks as task}
        <p>{task.text} {task.date}</p>
      {/each}
    {/if}
  </div>
</section>
