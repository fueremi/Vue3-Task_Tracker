<template>
  <header>
    <h1>{{ text }}</h1>
    <Button
      :text="showAddTask ? 'Close' : 'Add Task'"
      @button-click="toggleAddTask"
      :color="showAddTask ? 'red' : 'green'"
      v-show="homePage"
    />
  </header>
</template>

<script>
import Button from "@/components/Button";

import { computed } from "vue";
import { useRoute } from "vue-router";

export default {
  name: "Header",
  props: {
    text: String,
    showAddTask: Boolean,
  },
  components: {
    Button,
  },
  setup(props, { emit }) {
    const route = useRoute();

    const toggleAddTask = () => {
      emit("toggle-add-task");
    };

    const homePage = computed(() => {
      if (route.path === "/") {
        return true;
      } else {
        return false;
      }
    });

    return {
      homePage,
      toggleAddTask,
    };
  },
};
</script>

<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
}
</style>
