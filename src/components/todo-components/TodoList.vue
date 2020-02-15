<template>
    <div class='todo-list'>
        <transition-group name="fade" enter-active-class="animated fadeInUp" leave-active-class="animated fadeOutDown">
            <div v-for='( todo , index ) in filteredTodos' :key='todo.id'>
                <TodoItem :todo='todo' v-on:delete-todo='deleteTodoItem(index)'  />
            </div>
        </transition-group>
        <div class="my-4 d-flex align-items-center justify-content-start">
            <div class="form-check">
                <input class="form-check-input" @change='checkAll' type="checkbox" id="check-all">
                <label for="check-all">
                    Check All
                </label>
            </div>
            <div class='d-flex ml-5'>
                <button type='button' @click.prevent='filter = "all"' :class='{ active : filter == "all" }' class='btn btn-success mr-2'>All</button>
                <button type='button' @click.prevent='filter = "active"' :class='{ active : filter == "active" }' class='btn btn-success mr-2'>Active</button>
                <button type='button' @click.prevent='filter = "completed"' :class='{ active : filter == "completed" }' class='btn btn-success'>Completed</button>
            </div>
        </div>
    </div>
</template>

<script>
    import { EventBus } from '@/event-bus';
    import TodoItem from './TodoItem.vue'
    export default {
        name:'TodoList',
        components:{
            TodoItem
        },
        data(){
            return{
                filter:'all',
                searchValue:''
            }
        },
        props: {
            todos : {
                type: Array,
                required: true
            }
        },
        methods:{
            deleteTodoItem(index){
                this.todos.splice(index , 1);
            },
            checkAll(){
                this.todos.forEach( todo => {
                    return todo.completed = event.target.checked
                })
            }
        },
        created(){
            EventBus.$on('search-value', (value) => {
                this.searchValue = value
            });
        },
        computed:{
            filteredTodos(){
                if( this.filter == 'all' ){
                    return this.todos;
                }else if( this.filter == 'active' ){
                    return this.todos.filter( todo => !todo.completed )
                }else if( this.filter == 'completed' ){
                    return this.todos.filter( todo => todo.completed )
                }
                return this.todos.filter( todo => {
                    todo.title.toLowerCase().includes(
                        this.searchValue.toLowerCase()
                    )
                }); 
            }
        }
    }
</script>

<style lang='scss' scoped>
    @import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.2/animate.min.css");

    .todo-list{
        width: 70%;
        margin:30px auto;
    }

    .btn{
        &.active{
            background: #fd7e14 !important;
            color: #ffffff;
            border: none !important;
            box-shadow: none !important;
            transition: all .2s ease-in-out;
        }
    }
</style>