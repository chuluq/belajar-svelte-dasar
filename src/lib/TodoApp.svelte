<script>
  import Todo from "./Todo.svelte";

  let data = $state([]);
  let id = 0;

  function add(e) {
    e.preventDefault();

    const input = document.getElementById("todo");
    data.push({
      id: id++,
      name: input.value,
    });
    input.value = "";
  }

  function remove(id) {
    data = data.filter((item) => item.id !== id);
  }
</script>

<form>
  <input type="text" id="todo" />
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
