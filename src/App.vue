
<template>
    <div class="container">
        <div class="row" style="height: 200px;"></div>
        <div class="row">
            <div class="col-6 m-auto">
                <div class="todo-list ">
                    <div class="header d-flex">
                        <i :class="{downBtn:allCompleted}" @click="completeAll()" class="bi bi-chevron-down ps-4 "></i>
                        <input v-if="searchFeatures" type="text" class="input-text" v-model="search" placeholder="Search...">
                        <input v-else type="text" @keyup.enter="addTodo()" v-model="input" class="input-text"
                               placeholder="What needs to be done?" autocomplete="off">
                        <div class="me-5 search-icon">
                            <i @click="searchToggle()"  class="bi bi-search"></i>
                        </div>
                    </div>

                    <ul>
                        <todo-list v-model="todo.task"  @cancelEdit="cancelEdit(todo)"   @doneEdit="doneEdit(todo)"  @editTodo="editTodo(todo)"     @removeTodo="removeTodo(index)"   @todoShow="show(todo)"  v-for="(todo,index) in searchTodo" :key="todo.id" :todo="todo" :index="index"></todo-list>
                        <li class=" px-3 py-1 d-flex justify-content-between footer">
                            <div class="align-self-center item-left "><p class="mb-0">{{doneJob}} item left</p></div>
                            <div class="align-self-center">
                             <todo-btn  @filterTask="type=>tasks=type" filterTodos  ></todo-btn>
                            </div>
                            <div class="align-self-center">
                                <button @click="clearCompleted()" v-if="filterCompleted">Clear Completed</button>
                            </div>

                        </li>
                    </ul>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
    import TodoList from './components/TodoList.vue';
    import TodoBtn from './components/TodoBtn.vue';

    export default {
        name: 'App',
        components:{
            TodoList,
            TodoBtn
        },
        data() {
            return {
                checked: [],
                input: '',
                search: '',
                todoCache: '',
                completed: false,
                tasks: '',
                searchFeatures: false,
                todos: [
                    {
                        id: 1,
                        task: 'Home Work',
                        completed: false,
                        editing: false,
                    },
                    {
                        id: 2,
                        task: 'Work Out',
                        completed: false,
                        editing: false,
                    },
                    {
                        id: 3,
                        task: 'Go Shopping',
                        completed: false,
                        editing: false

                    },
                ]
            }
        },
        computed: {
            doneJob() {
                return this.todos.filter(todo => todo.completed === false).length;
            },

            allCompleted() {
                return this.todos.filter(todo => todo.completed === false).length == 0;
            },
            filterTodos() {
                if (this.tasks ==='active') {
                    return this.todos.filter(todo => !todo.completed)

                } else if (this.tasks === 'completed') {
                    return this.todos.filter(todo => todo.completed);
                }
                  else{
                  return this.todos;
                }

            },
            searchTodo(){
                if(this.search.trim()!==''){
                    if( this.filterTodos.filter(todo=>todo.task.toLowerCase().indexOf(this.search.toLowerCase()) !== -1)){
                        return this.filterTodos.filter(todo=>todo.task.toLowerCase().indexOf(this.search.toLowerCase()) !== -1);
                    }

                }
                return this.filterTodos;
            },
            filterCompleted() {
                return this.todos.filter(todo => todo.completed === true).length > 0
            }

        },
        methods: {
            searchToggle(){
                this.searchFeatures=!this.searchFeatures;

            },
            show(todo) {
                todo.completed = !todo.completed;
            },

            addTodo() {
               if(this.input.trim()!==''){
                   const newInput = {
                       id: new Date().toISOString(),
                       task: this.input,
                       completed: false,
                       editing: false,
                   };
                   this.todos.push(newInput);
                   this.input = '';
                   this.id++;
               }


            },
            completeAll() {
                this.completed = !this.completed;
                if (this.completed == true) {
                    this.todos.forEach(todo => todo.completed = true);
                } else {
                    this.todos.forEach(todo => todo.completed = false);

                }

            },
            clearCompleted() {
                this.todos = this.todos.filter(todo => !todo.completed);
            },
            cancelEdit(todo) {
                todo.task = this.todoCache;
                todo.editing = false;

            },
            removeTodo(id) {
                // const id=todo.id;
                // this.todos=this.todos.filter(todo=>todo.id!==id);
                this.todos.splice(id, 1);

            },
            editTodo(todo) {

                this.todoCache = todo.task;
                this.todos.filter(todo => todo.editing = false);
                todo.editing = !todo.editing;

            },
            doneEdit(todo) {
                todo.editing = !todo.editing;
            },


        },



    }
</script>


    <style scoped>
    ul {
        list-style: none;
        padding: 0;
        margin: 0;
    }

    .todo-item {
        border: 1px solid #e2e2e2;
        padding: 12px 25px;
        display: flex;
        justify-content: space-between;
    }

    .todo-list {
        box-shadow: 0 0 14px 7px #dee2e6;
    }

    .input-text {
        display: inline-block;
        width: 100%;
        border: none;
        outline: none;
        padding: 15px;
    }

    .bi-chevron-down {
        color: #c2c2c2;
        font-weight: bolder;
        font-size: 25px;
    }

    .downBtn {
        color: #333333 !important;
        font-weight: bolder;
        font-size: 25px;

    }
    .search-icon{
        font-size: 20px;
        color: #2e2e2e;
    }

    .active {
        border: 1px solid #dfdfdf !important;
        border-radius: 3px;
    }

    .header {
        justify-content: center;
        align-items: center;
        border-bottom: 2px solid #c2c2c2;

    }



</style>
