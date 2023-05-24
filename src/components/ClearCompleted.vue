<template>
  <div class="align-self-center">
    <button @click="$emit('clearCompleted')" >Clear Completed</button>
  </div>
</template>

<script>
export default {
  name: "ClearCompleted"
}
</script>

<style scoped>
button {
  border: 1px solid #4f1f1f;
  background: none;
  margin: 0 5px;
  color: #8b8b8b;
}
</style>