<template>
  <div class="container">
    <form @submit="addTodo">
      <input type="text" v-model="title" name="title" placeholder="Add Todo..." />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        title: this.title,
        completed: false
      };
      axios
        .post("https://5e4ea1866272aa0014230dcf.mockapi.io/vue/todos", newTodo)
        .then(res => {
          this.$emit("add-todo", res.data);
          // console.log(res);
        })
        .catch(err => console.log(err));

      this.title = "";
    }
  }
};
</script>

<style scoped>
.container {
  padding: 20px 0;
}

input[type="text"] {
  padding: 5px;
  height: 40px;
  border-radius: 0;
  border: 1px solid #000;
}
input[type="text"]:focus {
  box-shadow: 0px 0px 12px -3px rgba(0, 0, 0, 0.3);
}

input[type="submit"] {
  color: #fff;
  background-color: #000;
  outline: none;
}
input[type="submit"]:hover {
  color: #fff;
  background-color: #000;
  opacity: 0.8;
}
</style>
