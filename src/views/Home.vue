<template>
  <AddTask @add-task="addTask" v-show="showAddTask" />
  <Tasks
    :tasks="tasks"
    @delete-task="deleteTask"
    @toggle-reminder="toggleReminder"
  />
</template>

<script>
import AddTask from "@/components/AddTask";
import Tasks from "@/components/Tasks";

import { ref } from "vue";

export default {
  name: "Home",
  components: {
    AddTask,
    Tasks,
  },
  props: {
    showAddTask: Boolean,
  },
  setup() {
    const tasks = ref([]);

    const fetchTasks = async () => {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    };

    const fetchTask = async (id) => {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    };

    const onSetup = async () => {
      tasks.value = await fetchTasks();
    };

    const addTask = async (task) => {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();

      tasks.value = [...tasks.value, data];
    };

    const deleteTask = async (id) => {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (tasks.value = tasks.value.filter((task) => task.id !== id))
          : alert("Error deleting task!");
      }
    };

    const toggleReminder = async (id) => {
      const taskToToggle = await fetchTask(id);
      const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };
      console.log(updateTask);

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(updateTask),
      });

      const data = await res.json();

      tasks.value = tasks.value.map((task) => {
        return task.id === id ? { ...task, reminder: data.reminder } : task;
      });
    };

    onSetup();

    return {
      tasks,
      addTask,
      deleteTask,
      toggleReminder,
    };
  },
};
</script>
