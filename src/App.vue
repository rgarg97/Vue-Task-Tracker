<template>
  <div class="container">
    <Header @toggle-form="toggleForm" title="Task Tracker" :buttonText="buttonText"/>
    <div v-if="showForm">
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks :tasks="tasks" @delete-task="removeTask"/>
  </div>
</template>

<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";

export default {
  name: 'App',
  components: {
    AddTask,
    Header, Tasks
  },
  data() {
    return {
      tasks: [],
      showForm: false,
      buttonText: 'Add Task'
    }
  },
  async created() {
    const res = await fetch("http://localhost:5000/tasks")
    this.tasks = await res.json()
  },
  methods: {
    removeTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id)
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    toggleForm() {
      this.showForm = !this.showForm;
      this.buttonText = this.showForm ? 'Close': 'Add Task'
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
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
