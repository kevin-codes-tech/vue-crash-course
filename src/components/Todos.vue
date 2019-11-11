<template>
  <div class="todos">
    <TodoItem
      v-for="todo of todos"
      v-bind:key="todo.id"
      v-bind:todo="todo"
      v-on:del-todo="$emit('del-todo', todo.id)"
    />
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: ["todos"]
};
</script>

<style>
</style>