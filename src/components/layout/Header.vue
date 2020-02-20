<template>
  <header class="header">
    <h1>TodoList</h1>
    <div id="nav">
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
    </div>
  </header>
</template>

<script>
export default {
  nme: "Header"
};
</script>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background-color: black;
  color: white;
  font-size: 18px;
  height: 60px;
  line-height: 60px;
}
.header h1 {
  padding: 0;
  margin: 0;
  float: left;
}
#nav {
  float: right;
  padding: 0;
  margin-right: 20px;
}
#nav a {
  color: #fff;
  text-decoration: none;
}
#nav a:first-of-type {
  margin-right: 5px;
}
#nav a.router-link-active {
  color: #fff;
}
#nav a.router-link-exact-active {
  color: #42b983;
  text-decoration: underline;
}
</style>
