<template>
    <input type="text" @keyup.esc="$emit('cancelEdit',todo)" v-focus  @keyup.enter="$emit('doneEdit',todo)"   v-model="todo.task"   >

</template>

<script>
    const focus = {
        mounted: (el) => el.focus()
    };
    export default {

        directives: {
            focus
        },
        name: "EditTodo",
        props:['todo'],
    }
</script>

<style scoped>

</style>