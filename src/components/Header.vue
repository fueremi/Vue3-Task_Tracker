<template>
  <header>
    <h1>{{ text }}</h1>
    <Button
      :text="showAddTask ? 'Close' : 'Add Task'"
      @button-click="$emit('toggle-add-task')"
      :color="showAddTask ? 'red' : 'green'"
      v-show="homePage"
    />
  </header>
</template>

<script>
import Button from "@/components/Button";

export default {
  name: "Header",
  props: {
    text: String,
    showAddTask: Boolean,
  },
  components: {
    Button,
  },
  computed: {
    homePage() {
      if (this.$route.path === "/") {
        return true;
      } else {
        return false;
      }
    },
  },
  emits: ["toggle-add-task"],
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
