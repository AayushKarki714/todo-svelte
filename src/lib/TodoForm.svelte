<script>
  export let title, description, completed, todoId;
  export let addUpdateTodo;

  function handleFormSubmit() {
    addUpdateTodo();
  }
</script>

<form on:submit|preventDefault={handleFormSubmit}>
  <div class="form-group">
    <label for="title">Title</label>
    <input
      required
      id="title"
      type="text"
      bind:value={title}
      placeholder="Enter a todo title"
    />
  </div>

  <div class="form-group">
    <label for="description">Description</label>
    <textarea
      required
      id="description"
      bind:value={description}
      placeholder="Enter a todo description..."
    />
  </div>

  <div>
    <label for="completed">Completed</label>
    <input type="checkbox" id="completed" bind:checked={completed} />
  </div>

  <button type="submit">{todoId ? "Update" : "Add"}</button>
</form>

<style>
  form {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .form-group {
    display: flex;
    flex-direction: column;
    gap: 4px;
  }
</style>
