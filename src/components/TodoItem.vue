<template>

        <div>

            <input @click="$emit('showTodo',todo)" :id="todo.id" :value="todo.task"
                   type="checkbox" style="margin-right: 10px;" :checked="todo.completed" >
            <label :class="{completed:todo.completed}" @dblclick="$emit('editTodo',todo)" :value="todo.task"   >{{todo.task}} </label>



        </div>


</template>

<script>


    export default {
        name: "TodoItem",
        props:[
            'todo'
        ],


    }
</script>

<style scoped>
    .completed {
        text-decoration: line-through;
    }
</style>