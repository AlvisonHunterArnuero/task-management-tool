<template>
  <div>
    <form>
      <c-input
        class="inp"
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
  color: #000000;
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
