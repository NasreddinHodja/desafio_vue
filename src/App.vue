<template>
  <div id="main-container">
    <div class="header">
      <h1>TODOs</h1>
      <ButtonItem
        @btn-click="toggleAddTodo"
        :text="showAddTodo ? 'Close' : 'Add Todo'"
        :color="showAddTodo ? 'var(--red)' : 'var(--green)'"
      />
    </div>
    <div v-show="showAddTodo">
      <AddTodo @add-todo="addTodo" />
    </div>
    <TodoList @delete-todo="deleteTodo" :todos="todos" />
  </div>
</template>

<script>
import ButtonItem from "./components/ButtonItem.vue";
import TodoList from "./components/TodoList.vue";
import AddTodo from "./components/AddTodo.vue";

export default {
  name: "TodoApp",

  components: {
    ButtonItem,
    TodoList,
    AddTodo,
  },

  data() {
    return {
      todos: [],
      showAddTodo: false,
    };
  },

  methods: {
    toggleAddTodo() {
      this.showAddTodo = !this.showAddTodo;
    },

    async fetchTodos() {
      const res = await fetch("api/todos");
      return await res.json();
    },

    async fetchTodo(id) {
      const res = await fetch(`api/todos/${id}`);
      return await res.json();
    },

    async deleteTodo(id) {
      if (confirm("Delete Todo?")) {
        const res = await fetch(`api/todos/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.todos = this.todos.filter((todo) => todo.id !== id))
          : alert("Error deleting todo");
      }
    },

    async addTodo(newTodo) {
      const res = await fetch("api/todos", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(newTodo),
      });
      this.todos = [...this.todos, await res.json()];
    },
  },

  async created() {
    this.todos = await this.fetchTodos();
  },
};
</script>

<style>
:root {
  --bg: #282a36;
  --bg-light: #44475a;
  --fg: #f8f8f2;
  --orange: #ffb86c;
  --green: #50fa7b;
  --red: #ff5555;
  --yellow: #f1fa8c;
  --pink: #ff79c6;
  --purple: #bd93f9;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background: var(--bg);
  color: var(--fg);
  font-family: "Roboto Mono";
}

#main-container {
  margin: auto;
  max-width: 500px;
  padding: 10px;
}

h1 {
  color: var(--orange);
}

.btn {
  border-radius: 5px;
  border-color: var(--bg);
  padding: 10px;
}

.header {
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
}
</style>
