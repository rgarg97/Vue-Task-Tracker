<template>
  <header>
    <h1>{{ title }}</h1>
    <button class="btn" @click="toggleForm">{{ buttonText }}</button>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: {
    title: String,
    buttonText: String,
  },
  methods: {
    toggleForm() {
      this.$emit("toggle-form");
    }
  }
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>