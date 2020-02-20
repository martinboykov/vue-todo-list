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
        .post("http://5e4ea1866272aa0014230dcf.mockapi.io/vue/todos", newTodo)
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
form {
  /* display: flex; */
}
input[type="text"] {
  flex: 10;
  padding: 5px;
  height: 40px;
  transform: translateX(2px);
  border-radius: 0;
}

input[type="submit"] {
  flex: 3;
}
</style>
