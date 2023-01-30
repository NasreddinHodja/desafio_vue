<template>
  <div class="todo" @click="showFullTodo">
    <h3>
      {{ todo.name }}
      <i @click="$emit('delete-todo', todo.id)" class="fas fa-times"></i>
    </h3>
    <div v-show="showFull" class="full-todo">
      <p>{{ todo.description }}</p>
      <br />
      created:
      <div class="date">{{ todo.created }}</div>
      deadline:
      <div class="date">{{ todo.deadline }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",

  props: {
    todo: Object,
  },

  data() {
    return {
      showFull: false,
    };
  },

  methods: {
    showFullTodo() {
      this.showFull = !this.showFull;
    },
  },
};
</script>

<style scoped>
.fas {
  color: var(--red);
}

.todo {
  background: var(--bg-light);
  padding: 10px 20px;
  margin-top: 10px;
  border-radius: 5px;
}

h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: var(--yellow);
}

.date {
  color: var(--purple);
}
</style>
