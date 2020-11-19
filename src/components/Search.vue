<template>
  <div>
    <form>
      <c-input
        type="text"
        placeholder="Search your task here"
        id="txtSearch"
        w="100%"
        m="2"
        size="lg"
        v-model="query"
        v-on:input="$emit('search-task', query)"
      />
    </form>
  </div>
</template>
<script>
import { CInput } from "@chakra-ui/vue";
export default {
  name: "Search",
  data() {
    return {
      query: "",
    };
  },

  components: { CInput },
};
</script>

<style scoped></style>
