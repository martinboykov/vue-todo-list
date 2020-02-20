<template>
  <div id="app">
    <div class="main">
      <AddTodo v-on:add-todo="addTodo"></AddTodo>
      <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    </div>
  </div>
</template>

<script>
import axios from "axios";

import Todos from "../components/Todos.vue";
import AddTodo from "../components/AddTodo.vue";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(todo) {
      axios
        .delete(`https://5e4ea1866272aa0014230dcf.mockapi.io/vue/todos/${todo.id}`)
        .then(() => {
           this.todos.splice(todo.index, 1);
        })
        .catch(err => console.log(err));
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
    }
  },

  created() {
    axios
      .get("https://5e4ea1866272aa0014230dcf.mockapi.io/vue/todos")
      .then((res) => {
        this.todos = res.data;
      })
      .catch(err => console.log(err));
  },
  mounted() {
    return console.log("mounted");
  },
  updated() {
    return console.log("updated");
  },
  destroyed() {
    return console.log("destroyed");
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
  background-color: #555;
  color: #fff;
  padding: 0 20px;
  height: 40px;
  cursor: pointer;
}

.btn:hover {
  background-color: #666;
  color: #000;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.main {
  margin-top: 60px;
}
</style>
