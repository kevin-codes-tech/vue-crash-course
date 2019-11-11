<template>
  <div class="todo-item">
    <p v-bind:class="{'is-complete': todo.completed}">
      <span>
        <input type="checkbox" v-on:change="toggleComplete" v-bind:checked="todo.completed" />
      </span>
      {{todo.title}}
      <span>
        <button class="deleted" @click="$emit('del-todo', todo.id)">X</button>
      </span>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    toggleComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.is-complete {
  text-decoration: line-through;
}

.deleted {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>