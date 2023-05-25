<script>
  import './app.css'
  import {
    todoSelectors,
    addTodo,
    removeTodo,
    fetchRandomTodo
  } from "./store/slices/todoSlice";
  import { store, useSelector } from "./store/store";

  $: todoList = useSelector(
    todoSelectors.todos,
    newList => (todoList = newList)
  );

  $: todoListLoading = useSelector(
    todoSelectors.loading,
    newLoading => (todoListLoading = newLoading)
  );

  let newTodo;
</script>

<style>
  
</style>

<main class="text-center">
  <h1 class="text-2xl text-red-400 uppercase font-light my-2">Todos using Svelte and redux-toolkit</h1>
  <hr class="my-2"/>
  <div class="flex justify-center">
    <input class="border" bind:value={newTodo} />
    <button class="text-gray-200 bg-gray-800 ml-2 px-2 hover:bg-gray-200 hover:text-gray-800" on:click={() => store.dispatch(addTodo(newTodo))}>Add Todo</button>
  </div>
  
  <button class="btn" on:click={() => store.dispatch(fetchRandomTodo())}>
    Add Random Todo (API)
  </button>
  {#if todoListLoading}
    <h1>Loading...</h1>
  {/if}

  <ul>
    {#each todoList as todo}
      <li>
        {todo} -
        <button class="btn" on:click={() => store.dispatch(removeTodo(todo))}>
          Remove
        </button>
      </li>
    {/each}
  </ul>
</main>
