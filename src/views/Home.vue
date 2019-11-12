<template>
  <div id="home">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import AddTodo from "@/components/AddTodo";
import Todos from "@/components/Todos";
export default {
  name: "Home",
  components: {
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
        method: "DELETE",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json"
        }
      })
        .then(responseData => responseData.json())
        .then(() => (this.todos = this.todos.filter(todo => todo.id !== id)));
    },
    addTodo(newTodo) {
      fetch("https://jsonplaceholder.typicode.com/todos", {
        method: "POST",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json"
        },
        body: JSON.stringify(newTodo)
      })
        .then(responseData => responseData.json())
        .then(response => (this.todos = [...this.todos, response]));
    }
  },
  created() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(responseData => responseData.json())
      .then(response => (this.todos = response));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #ffffff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
