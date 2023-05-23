<template>
    <div @click="$emit('removeTodo',index)" class="delete-btn text-danger">
        <i class="bi bi-x-lg pe-3" style="cursor: pointer;"></i>
    </div>
</template>

<script>
    export default {
        name: "RemoveTodo",
        props:['todo','index'],
    }
</script>

<style scoped>

</style>