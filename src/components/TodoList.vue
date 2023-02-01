<template>
  <div :key="todo.id" v-for="todo in todos">
    <TodoItem @delete-todo="$emit('delete-todo', todo.id)" :todo="todo" />
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "TodoList",

  props: {
    todos: Array,
  },

  components: {
    TodoItem,
  },

  emits: ["delete-todo"],
};
</script>

<style scoped></style>
