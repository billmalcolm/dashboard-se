<script>
  import Weather from "./components/Weather.svelte";
  import TodoList from "./components/TodoList.svelte";

  if (localStorage.getItem("Tasks") === null) {
    localStorage.setItem("Tasks", "");
  }
</script>

<style>
  main {
    display: flex;
    justify-content: space-between;
    padding: 5%;
    text-align: center;

    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<Weather />
<main>
  <TodoList />
</main>
