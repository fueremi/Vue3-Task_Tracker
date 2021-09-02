<template>
  <div class="container">
    <Header text="Task Tracker" />
    <Tasks
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-reminder="toggleReminder"
    />
  </div>
</template>

<script>
import Header from "@/components/Header";
import Tasks from "@/components/Tasks";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    deleteTask(id) {
      if (confirm("Are you sure?")) {
        this.tasks = this.tasks.filter((task) => {
          return task.id !== id;
        });
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => {
        return task.id === id ? { ...task, reminder: !task.reminder } : task;
      });
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        task: "Learn Vue 3 Composition API",
        date: "Sep 5th at 9.30am",
        reminder: true,
      },
      {
        id: 2,
        task: "Learn Quasar",
        date: "Sep 6th at 9.30am",
        reminder: true,
      },
      {
        id: 3,
        task: "Fixing hosting email issue",
        date: "Sep 8th at 9.30am",
        reminder: false,
      },
    ];
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
