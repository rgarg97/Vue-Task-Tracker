<template>
  <div :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3>{{ task.text }}<i class="fas fa-times" @click="removeTask"></i></h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object
  },
  methods: {
    async removeTask() {
      const res = await fetch(`http://localhost:5000/tasks/${this.task.id}`, {"method": "DELETE"})
      this.$emit("delete-task", this.task.id)
    }
  },
  emits: ["delete-task"],
}
</script>

<style scoped>
.fas {
  color: red;
}
div {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>