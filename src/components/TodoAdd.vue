<template>
  <div>
    <form v-on:submit="addTask">
      <c-input
        class="inp"
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

<style scoped>
.inp {
  display: flex;
  -webkit-box-align: center;
  align-items: center;
  position: relative;
  -webkit-appearance: none;
  font-size: 1rem;
  padding-left: 1rem;
  padding-right: 1rem;
  height: 2.5rem;
  line-height: 2.5rem;
  color: #242423;
  background-color: rgba(255, 255, 255, 0.7);
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial,
    sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  transition: all 0.2s ease 0s;
  outline: none;
  border-radius: 0.25rem;
  border-width: 2px;
  border-style: solid;
  border-image: initial;
  border-color: transparent;
}
</style>
