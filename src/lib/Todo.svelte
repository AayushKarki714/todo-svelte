<script>
  export let completed, title, description;
  export let deleteTodo;
  export let editTodo;

  let count = 0;

  $: {
    setTimeout(() => {
      count += 1;
    }, 1000);
  }
</script>

<li>
  <h2 class:completed>{title} ({count})</h2>
  <p class:completed>
    {description}
  </p>

  <div>
    <button on:click={editTodo}>Edit</button>
    <button on:click={deleteTodo}>Delete</button>
  </div>
</li>

<style>
  .completed {
    text-decoration: line-through;
  }
</style>
