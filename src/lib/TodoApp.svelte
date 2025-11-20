<script>
  import EditTodo from "./EditTodo.svelte";
  import Todo from "./Todo.svelte";
  import { fade, fly } from "svelte/transition";

  let data = $state([]);
  let name = $state("");
  let id = 0;

  function add(e) {
    e.preventDefault();

    data.push({ id: id++, name: name });
    name = "";
  }

  function remove(id) {
    data = data.filter((item) => item.id !== id);
  }

  function edit(id) {
    for (let i = 0; i < data.length; i++) {
      if (data[i].id === id) {
        data[i] = { ...data[i], edit: true };
      }
    }
  }

  function onEdit(id, name) {
    for (let i = 0; i < data.length; i++) {
      if (data[i].id === id) {
        data[i] = { id, name, edit: false };
      }
    }
  }
</script>

<form>
  <input type="text" id="todo" bind:value={name} />
  <button onclick={add}>Add</button>
</form>

<ul>
  {#each data as todo (todo.id)}
    <li
      in:fly={{ y: -200, duration: 1000 }}
      out:fly={{ y: 200, duration: 1000 }}
      onintrostart={() => console.log("intro start")}
      onintroend={() => console.log("intro end")}
      onoutrostart={() => console.log("outro start")}
      onoutroend={() => console.log("outro end")}
    >
      {#if todo.edit}
        <EditTodo id={todo.id} name={todo.name} onedit={onEdit} />
      {:else}
        <Todo {...todo} />
        <button onclick={() => edit(todo.id)}>Edit</button>
        <button onclick={() => remove(todo.id)}>Remove</button>
      {/if}
    </li>
  {/each}
</ul>

<style>
  :global {
    button {
      background-color: #007bff;
      color: #fff;
      padding: 10px 20px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }

    button:hover {
      background-color: #0056b3;
    }

    button:focus {
      outline: none;
      box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.5);
    }
  }
</style>
