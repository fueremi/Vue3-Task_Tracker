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

export default {
  name: "Home",
  components: {
    AddTask,
    Tasks,
  },
  props: {
    showAddTask: Boolean,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async addTask(payload) {
      console.log(JSON.stringify(payload));
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(payload),
      });
      const data = await res.json();

      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error deleting task!");
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);
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

      this.tasks = this.tasks.map((task) => {
        return task.id === id ? { ...task, reminder: data.reminder } : task;
      });
    },
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>
