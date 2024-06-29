<script>
  import Todo from "./lib/Todo.svelte";
  import TodoForm from "./lib/TodoForm.svelte";
  import TodoList from "./lib/TodoList.svelte";
  import TodoStatusFilter from "./lib/TodoStatusFilter.svelte";

  let todos = localStorage.getItem("todos")
    ? JSON.parse(localStorage.getItem("todos"))
    : [];

  let title = "";
  let description = "";
  let completed = false;

  let todoId;
  let status = "";

  function addUpdateTodo() {
    if (todoId) {
      todos = todos.map((todo) => {
        if (todo.id === todoId) {
          return { ...todo, title, description, completed };
        }
        return todo;
      });
    } else {
      const todo = { id: Date.now(), title, description, completed };
      todos = [todo, ...todos];
    }
    todoId = undefined;
    title = description = "";
    completed = false;
  }

  function editTodo(todo) {
    todoId = todo.id;
    title = todo.title;
    description = todo.description;
    completed = todo.completed;
  }

  function deleteTodo(todoId) {
    todos = todos.filter((todo) => todo.id !== todoId);
  }

  $: {
    localStorage.setItem("todos", JSON.stringify(todos));
  }

  $: filteredTodos = todos.filter((todo) => {
    if (status === "") {
      return todo;
    }
    return todo.completed === status;
  });
</script>

<TodoForm {addUpdateTodo} {todoId} bind:completed bind:title bind:description />
<TodoStatusFilter bind:status />
<TodoList todos={filteredTodos}>
  {#each filteredTodos as todo (todo.id)}
    <Todo
      {...todo}
      editTodo={() => editTodo(todo)}
      deleteTodo={() => deleteTodo(todo.id)}
    />
  {/each}
</TodoList>
