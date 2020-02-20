<template>
  <div class="container">
    <div v-bind:key="todo.id" v-for="(todo, index) in todos">
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', { index:index, id: todo.id })" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: ["todos"]
};
</script>

<style scoped>
.container {
  max-width: 1366px;
  width: 100%;
  margin: 0 auto;
}
</style>
