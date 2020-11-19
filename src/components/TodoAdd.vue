<template>
  <div>
    <form v-on:submit="addTask">
      <c-input
        type="text"
        w="100%"
        m="2"
        size="lg"
        v-model="title"
        placeholder="Type in your task"
      />
    </form>
  </div>
</template>
<script>
import { CInput } from "@chakra-ui/vue";
import { uuid } from "vue-uuid";
export default {
  name: "TodoAdd",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTask(e) {
      e.preventDefault();
      const newTask = {
        id: uuid.v4(),
        title: this.title,
        completed: false,
      };
      this.title = "";
      this.$emit("add-task", newTask);
    },
  },
  components: { CInput },
};
</script>

<style scoped></style>
