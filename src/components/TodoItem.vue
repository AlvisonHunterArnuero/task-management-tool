<template>
  <div>
    <c-box
      font-weight="semibold"
      letter-spacing="wide"
      font-size="xs"
      text-transform="uppercase"
      d="flex"
      align-items="baseline"
      bg="gray.700"
      w="100%"
      mb="2"
      p="4"
      color="white"
      border-width="0px"
      rounded="lg"
      overflow="hidden"
    >
      <c-box w="95%" v-bind:class="{ completed: todo.completed }">
        <c-checkbox
          size="sm"
          v-bind:is-checked="todo.completed"
          v-on:change="taskCompleted"
        >
          {{ todo.title }}
        </c-checkbox>
      </c-box>

      <c-box w="5%">
        <c-icon-button
          aria-label="Search database"
          icon="minus"
          size="sm"
          isRound="true"
          variant="solid"
          variant-color="red"
          v-on:click="$emit('delete-task', todo.id)"
        />
      </c-box>
    </c-box>
  </div>
</template>
<script>
import { CBox, CCheckbox, CIconButton } from "@chakra-ui/vue";
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    taskCompleted() {
      this.todo.completed = !this.todo.completed;
    },
  },
  components: { CBox, CCheckbox, CIconButton },
};
</script>

<style scoped>
.completed {
  color: #ffba08;
  text-decoration: line-through;
}
</style>
