<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todoslist">
      <TodoItem v-bind:todo="todo" />
    </div>
  </div>
</template>
<script>
import TodoItem from './TodoItem'
export default {
  name: "Todos",
  props: ["todoslist"],
  components:{TodoItem}
};
</script>

<style scoped></style>
