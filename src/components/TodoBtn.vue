<template>
    <button @click="$emit('filterTask', 'all')" class="active">All</button>
    <button @click="$emit('filterTask', 'active')" >Active</button>
    <button @click="$emit('filterTask', 'completed')">Completed</button>

</template>

<script>
    export default {
        name: "TodoBtn",


      emits:['filterTask']

    }
</script>

<style scoped>
.footer button {
  border: 1px solid white;
  background: none;
  outline: none;
  margin: 0 5px;
  color: #8b8b8b;
}

.footer button:hover {
  border: 1px solid #dfdfdf;
  border-radius: 3px;
}


</style>