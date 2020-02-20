<template>
  <div class="todo-item">
    <div class="checkbox-group">
      <label class="checkbox privacy-label" v-bind:class="{'is-complete': todo.completed}">
        {{todo.title}}
        <input type="checkbox" v-on:change="markComplete" :checked="todo.completed" />
        <span class="checkmark"></span>
      </label>
      <button @click="$emit('del-todo', todo.id)" class="del">&times;</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
      console.log(this.todo.completed);
      axios
        .put(
          `https://5e4ea1866272aa0014230dcf.mockapi.io/vue/todos/${this.todo.id}`,
          this.todo
        )
        .then()
        .catch(err => console.log(err));
    }
  }
};
</script>

<style scoped>
.del {
  font-size: 20px;
  background-color: #ff0000;
  color: #fff;
  border: none;
  padding: 2px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
  outline: none;
}
.is-complete {
  text-decoration: line-through;
}
.todo-item {
  background-color: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
.todo-item::after {
  content: "";
  clear: both;
  display: table;
}
.checkbox-group::after {
  content: "";
  clear: both;
  display: table;
}
.checkbox-group input {
  display: none;
}
.checkbox-group label.checkbox {
  font-size: 20px;
  color: #303030;
  padding: 0 0 0 35px;
  position: relative;
  display: block;
  cursor: pointer;
  user-select: none;
  text-align: left;
  float: left;
}

.checkbox-group label.checkbox .checkmark {
  position: absolute;
  top: 3px;
  left: 0;
  height: 20px;
  width: 20px;
  border: 2px solid #303030;
}
.checkbox-group label.checkbox .checkmark:after {
  display: none;
  content: "";
  position: absolute;
  left: 5px;
  top: 1px;
  width: 4px;
  height: 8px;
  border: solid #303030;
  border-width: 0 3px 3px 0;
  transform: rotate(45deg);
}

.checkbox-group label.checkbox input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}
.checkbox-group label.checkbox input:checked ~ .checkmark:after {
  display: block;
}

.checkbox-group a {
  text-decoration: underline;
}
</style>
