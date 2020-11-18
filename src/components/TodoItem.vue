<template>
  <div>
    <div class="todo-body" v-bind:class="{ completed: todo.completed }">
      <input type="checkbox" />
      {{ todo.title }}
    </div>

    <div class="todo-action">
      <button>Eliminar</button>
      {{ todo.title }}
    </div>
  </div>
</template>
<script>
export default {
  name: "TodoItem",
  props: ["todo"],
};
</script>

<style scoped>
.completed {
  color: red;
}
</style>
