<template>
  <div>
    <div id="header"></div>
    <div id="main-container">
      <h1 class="">Todos</h1>
      <Todos v-bind:todoslist="copyTodos" />
      <Search />
      <TodoAdd />
    </div>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
import Todos from "./components/Todos.vue";
import TodoAdd from "./components/TodoAdd.vue";

export default {
  name: "App",
  components: {
    Search,
    Todos,
    TodoAdd,
  },
  data() {
    return {
      todos: [
        {
          id: 0,
          title: "Comprar la Cena",
          completed: false,
        },
        {
          id: 1,
          title: "Barrer el Cuarto",
          completed: true,
        },
        {
          id: 2,
          title: "Arreglar la cama",
          completed: false,
        },
        {
          id: 3,
          title: "Estudiar Python",
          completed: true,
        },
      ],
      copyTodos: [],
    };
  },
  created() {
    this.copyTodos = [...this.todos];
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
