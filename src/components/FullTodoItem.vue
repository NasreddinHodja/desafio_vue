<template>
  <div>
    <h3>
      {{ todo.name }}
      <i @click="$emit('delete-todo', todo.id)" class="fas fa-times"></i>
    </h3>
  </div>
</template>

<script>
export default {
  name: "FullTodoItem",

  props: {
    todo: Object,
  },
};
</script>

<style scoped>
.fas {
  color: var(--red);
}

div {
  background: var(--bg-light);
  padding: 10px 20px;
  margin-top: 10px;
  border-radius: 5px;
}

h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
