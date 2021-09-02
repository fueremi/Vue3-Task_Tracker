<template>
  <div v-for="task in tasks" :key="task.id">
    <h3>{{ task.task }}</h3>
  </div>
</template>

<script>
export default {
  name: "Tasks",
  props: {
    tasks: Array,
  },
};
</script>
