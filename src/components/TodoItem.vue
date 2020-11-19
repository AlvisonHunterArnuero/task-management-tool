<template>
  <div>
    <c-box
      font-weight="semibold"
      letter-spacing="wide"
      font-size="xs"
      text-transform="uppercase"
      ml="2"
      d="flex"
      align-items="baseline"
      bg="gray.700"
      w="100%"
      mb="1"
      p="4"
      color="white"
    >
      <c-box w="90%" v-bind:class="{ completed: todo.completed }">
        <c-checkbox
          size="md"
          v-bind:default-is-checked="todo.completed"
          v-on:change="taskCompleted"
        >
          {{ todo.title }}
        </c-checkbox>
      </c-box>

      <c-box w="10%">
        <c-button
          v-on:click="$emit('delete-task', todo.id)"
          variant-color="red"
        >
          Delete
        </c-button>
      </c-box>
    </c-box>
  </div>
</template>
<script>
import { CBox, CCheckbox, CButton } from "@chakra-ui/vue";
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    taskCompleted() {
      this.todo.completed = !this.todo.completed;
    },
  },
  components: { CBox, CCheckbox, CButton },
};
</script>

<style scoped>
.completed {
  color: lime;
}
</style>
