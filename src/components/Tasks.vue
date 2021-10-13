<template>
  <div :key="task.id" v-for="task in tasks">
    <Task :task="task" @delete-task="removeTask"/>
  </div>
</template>

<script>
import Task from "./Task";
export default {
  name: "Tasks",
  components: {Task},
  props: {
    tasks: Array
  },
  methods: {
    async removeTask(id) {
      this.$emit("delete-task", id);
    }
  },
  emits: ["delete-task"],
}
</script>

<style scoped>
</style>