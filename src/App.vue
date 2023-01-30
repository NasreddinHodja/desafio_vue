<template>
  <div id="main-container">
    <h1>Todo app</h1>
    <ButtonItem
      @btn-click="toggleAddTodo"
      :text="showAddTodo ? 'Close' : 'Add Todo'"
      :color="showAddTodo ? 'var(--red)' : 'var(--green)'"
    />
    <div v-show="showAddTodo">
      <AddTodo @add-todo="addTodo" />
    </div>
    <TodosItem @delete-todo="deleteTodo" :todos="todos" />
  </div>
</template>

<script>
import ButtonItem from "./components/ButtonItem.vue";
import TodosItem from "./components/TodosItem.vue";
import AddTodo from "./components/AddTodo.vue";

export default {
  name: "TodoApp",

  components: {
    ButtonItem,
    TodosItem,
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

    deleteTodo(id) {
      if (confirm("Delete Todo?")) {
        this.todos = this.todos.filter((todo) => todo.id !== id);
      }
    },

    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    },
  },

  created() {
    this.todos = [
      {
        id: 1,
        name: "text 1",
        description: "test 1 test 1",
        created: "20/01/2023",
        deadline: "22/01/2023",
      },
      {
        id: 2,
        name: "text 2",
        description: "test 2 test 2",
        created: "20/01/2023",
        deadline: "22/01/2023",
      },
      {
        id: 3,
        name: "text 3",
        description: "test 3 test 3",
        created: "20/01/2023",
        deadline: "22/01/2023",
      },
    ];
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
</style>
