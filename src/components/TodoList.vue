<template>
    <li class="todo-item">
        <todo-item  @editTodo="editTodo(todo)" @showTodo="ShowTodo(todo)" :todo="todo" v-if="!todo.editing"></todo-item>
        <edit-todo  @cancelEdit="$emit('cancelEdit',todo)" @doneEdit="$emit('doneEdit',todo)" :todo="todo" v-else ></edit-todo>
        <remove-todo @removeTodo="$emit('removeTodo',index)" :index="index" :todo="todo"></remove-todo>
    </li>
</template>

<script>
    import TodoItem from './TodoItem.vue';
    import EditTodo from './EditTodo.vue';

    import RemoveTodo from './RemoveTodo.vue';
    export default {
        name: "TodoList",
        components: {
            TodoItem,
            RemoveTodo,
            EditTodo
        },
        props: ['todo','index'],
        methods: {
            ShowTodo(todo) {
                this.$emit('todoShow', todo);
            },
            editTodo(todo){
                this.$emit('editTodo',todo);
            }
        }
    }
</script>

<style scoped>

</style>