<template>
  <c-theme-provider>
    <c-reset />

    <div class="container">
      <c-stack :spacing="5">
        <c-box :p="5" shadow="md" my="4" border-width="1px" rounded="lg">
          <c-heading
            class="header_title"
            color="gray.500"
            text-transform="uppercase"
            as="h1"
            justify-content="center"
          >
            Aufgabenliste - Task Management Tool
          </c-heading>
          <c-text :mt="4" color="white" font-size="xl">
            Aufgabenliste is one of the top-rated and trusted task management
            tools by more than 50 organizations across the globe. As it is a
            dedicated project management and team collaboration tool, you will
            get all the leading features that you need to manage your tasks and
            projects efficiently.This paragraph is, of course, totally
            fake.</c-text
          >
        </c-box>
      </c-stack>

      <c-box d="flex" flex-dir="column">
        <c-accordion
          :allow-toggle="true"
          bg="gray.800"
          mb="4"
          border-width="0px"
          rounded="lg"
        >
          <c-accordion-item>
            <c-accordion-header>
              <c-box flex="1" text-align="left">
                <c-text fontSize="15px" class="acordion-item-title"
                  >SEARCH TASK:</c-text
                >
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
                <c-text fontSize="15px" class="acordion-item-title"
                  >ADD NEW TASK</c-text
                >
              </c-box>
              <c-accordion-icon />
            </c-accordion-header>
            <c-accordion-panel pb="4">
              <TodoAdd v-on:add-task="addTask" />
            </c-accordion-panel>
          </c-accordion-item>
        </c-accordion>
        <div v-show="!copyTodos.length">
          <c-alert status="error" text-transform="uppercase">
            <c-alert-icon />
            Requested Task does not exist on current Tasks List. Please try
            again with another word.
          </c-alert>
        </div>

        <Todos v-bind:todoslist="copyTodos" v-on:delete-task="deleteTask" />
      </c-box>
      <c-box flex="1" m="4" text-align="center" color="white"
        >Aufgabenliste. Made with ❤️ in VueJS - Powered by Alvison Hunter. Last
        Updated on November 19th, 2020.</c-box
      >
    </div>
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
  CStack,
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
    CStack,
    Search,
    Todos,
    TodoAdd,
  },
  methods: {
    addTask(newtask) {
      this.todos.push(newtask);
      this.copyTodos = [...this.todos];
      this.showToast("Item Created!", "Task has been successfully created.");
    },
    deleteTask(id) {
      this.todos = this.todos.filter((task) => task.id !== id);
      this.copyTodos = [...this.todos];
      this.showToast("Item Deleted!", "Task has been successfully deleted.");
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

<style>
body {
  height: 100vh;
  margin: 0;
  padding: 0px;
  background-color: rgb(26, 32, 44);
  color: rgba(255, 255, 255, 0.92);
  width: 100%;
}
#app {
  display: flex;
  height: 100%;
}
.container {
  margin: auto;
  margin-top: 3rem;
  width: 90%;
  padding: 20px;
}
.header_title {
  color: #fff3b0;
  font-family: system-ui, Georgia, serif;
  font-size: 2.3rem;
  text-align: left;
}
</style>
