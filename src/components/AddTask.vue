<template>
  <form @submit.prevent="onSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input type="text" v-model="task" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="text"
        v-model="date"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<script>
import { ref } from "vue";

export default {
  name: "AddTask",
  setup(props, { emit }) {
    const task = ref("");
    const date = ref("");
    const reminder = ref(false);

    const onSubmit = () => {
      if (!task.value) {
        alert("Please add a task!");
        return;
      }

      const newTask = {
        task: task.value,
        date: date.value,
        reminder: reminder.value,
      };

      emit("add-task", newTask);

      task.value = "";
      date.value = "";
      reminder.value = false;
    };

    return {
      task,
      date,
      reminder,
      onSubmit,
    };
  },
};
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>
