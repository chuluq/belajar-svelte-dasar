<script>
  import Todo from "./Todo.svelte";

  let data = $state([]);
  let id = 0;
  let inputValue = $state("");

  function add(e) {
    e.preventDefault();

    if (inputValue.trim()) {
      data.push({
        id: id++,
        name: inputValue,
      });
      inputValue = "";
    }
  }

  function remove(id) {
    data = data.filter((item) => item.id !== id);
  }
</script>

<form>
  <input type="text" bind:value={inputValue} />
  <button onclick={add}>Add</button>
</form>

<ul>
  {#each data as todo (todo.id)}
    <li>
      <Todo {...todo} />
      <button onclick={() => remove(todo.id)}>Remove</button>
    </li>
  {/each}
</ul>
