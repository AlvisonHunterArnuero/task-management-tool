<template>
  <c-theme-provider>
    <c-reset />
    <c-box w="100%">
      <div>
        <c-heading
          m="4"
          color="yellow.100"
          text-transform="uppercase"
          as="h1"
          size="lg"
        >
          Task Management Tool
        </c-heading>

        <c-accordion bg="gray.200">
          <c-accordion-item>
            <c-accordion-header>
              <c-box flex="1" text-align="left">
                <c-text fontSize="20px" color="gray.500">SEARCH TASK:</c-text>
              </c-box>
              <c-accordion-icon />
            </c-accordion-header>
            <c-accordion-panel pb="4">
              <Search v-on:search-task="searchTask" />
            </c-accordion-panel>
          </c-accordion-item>
          <c-accordion-item>
            <c-accordion-header>
              <c-box flex="1" text-align="left">
                <c-text fontSize="20px" color="gray.500">ADD NEW TASK</c-text>
              </c-box>
              <c-accordion-icon />
            </c-accordion-header>
            <c-accordion-panel pb="4">
              <TodoAdd v-on:add-task="addTask" />
            </c-accordion-panel>
          </c-accordion-item>
        </c-accordion>
        <div v-show="!copyTodos.length">
          <c-alert status="error">
            <c-alert-icon />
            Requested query does not exist on current Tasks DB. Please try
            again.
          </c-alert>
        </div>

        <Todos v-bind:todoslist="copyTodos" v-on:delete-task="deleteTask" />
      </div>
    </c-box>
  </c-theme-provider>
</template>

<script>
import {
  CHeading,
  CThemeProvider,
  CReset,
  CBox,
  CText,
  CAccordion,
  CAccordionItem,
  CAccordionHeader,
  CAccordionPanel,
  CAccordionIcon,
  CAlert,
  CAlertIcon,
} from "@chakra-ui/vue";
import Search from "./components/Search.vue";
import Todos from "./components/Todos.vue";
import TodoAdd from "./components/TodoAdd.vue";
import json from "@/assets/data.json";

export default {
  name: "App",
  components: {
    CHeading,
    CThemeProvider,
    CReset,
    CBox,
    CText,
    CAccordion,
    CAccordionItem,
    CAccordionHeader,
    CAccordionPanel,
    CAccordionIcon,
    CAlert,
    CAlertIcon,
    Search,
    Todos,
    TodoAdd,
  },
  methods: {
    addTask(newtask) {
      this.todos.push(newtask);
      this.copyTodos = [...this.todos];
      this.showToast("Task Created!", "Task has been successfully created.");
    },
    deleteTask(id) {
      this.todos = this.todos.filter((task) => task.id !== id);
      this.copyTodos = [...this.todos];
      this.showToast("Task Deleted!", "Task has been successfully deleted.");
    },
    searchTask(query) {
      //If the given str has no values, keep the array intact
      if (query.trim() === "") {
        this.copyTodos = [...this.todos];
      }
      // if not, let's filter the task with the given str
      else {
        let queryResult = this.todos.filter((task) => {
          return task.title.toLowerCase().includes(query.toLowerCase());
        });
        this.copyTodos = [...queryResult];
      }
    },

    showToast(argTitle, argDescription) {
      this.$toast({
        title: argTitle,
        description: argDescription,
        status: "success",
        duration: 4000,
      });
    },
  },
  data() {
    return {
      todos: json.todos,
      copyTodos: [],
    };
  },
  created() {
    this.copyTodos = [...this.todos];
  },
};
</script>
<style scoped></style>
