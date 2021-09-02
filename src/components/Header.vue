<template>
  <header>
    <h1>{{ text }}</h1>
    <Button text="Add Task" color="#005511" />
  </header>
</template>

<script>
import Button from "@/components/Button";

export default {
  name: "Header",
  props: {
    text: String,
  },
  components: {
    Button,
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
