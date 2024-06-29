<script>
  export let todos;
</script>

{#if !!todos.length}
  <ul><slot /></ul>
{:else}
  <p>Not todos found...</p>
{/if}
