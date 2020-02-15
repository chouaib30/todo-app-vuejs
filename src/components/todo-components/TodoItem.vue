<template>
    <div class='todo-item d-flex align-items-center '>
        <div class='d-flex w-75 align-items-center justify-content-start'>
            <input type='checkbox' class='form-control w-25 d-flex justify-content-start'  :checked='todo.completed' @change='markAsComplete' name='todo-check'>
            <label v-if='!todo.edit' @dblclick.prevent='editTodo' class='d-block w-75 text-left mb-0 justify-content-start' :class='{ completed: todo.completed }'>{{ todo.title }}</label>
            <input v-else class='form-control p-4' @blur='doneEdit' @keyup.enter='doneEdit' @keyup.esc='cancelEdit' type='text' v-model='todo.title'>
        </div>
        <div class='d-flex w-25 justify-content-end'>
            <button class='btn btn-danger' @click.prevent="deleteTodo">Delete</button>
        </div>
    </div>
</template>

<script>
    export default {
        name:'TodoItem',
        props:{
            todo:{
                type: Object,
                required: true
            }
        },
        data(){
            return {
                titleBeforeCached : this.todo.title
            }
        },
        methods :{
            // Mark as Completed Todo Item 
            markAsComplete(){
                return this.todo.completed = !this.todo.completed
            },
            // Delete Todo Item 
            deleteTodo(){
                this.$emit('delete-todo')
            },
            // Edit Todo Item 
            editTodo(){
                this.todo.edit = true
                this.titleBeforeCached = this.todo.title
            },
            // Done Edit Todo Item 
            doneEdit(){
                if( this.todo.title == '' ){
                    return this.todo.title = this.titleBeforeCached
                }
                this.todo.edit = false
            },
            // Cancel Edit Todo Item 
            cancelEdit(){
                this.todo.title = this.titleBeforeCached
                this.todo.edit = false
            }
        }
    }
</script>

<style lang='scss' scoped>
    .todo-item{
        background: #ffffff;
        margin:5px auto;
        padding: 20px;
        box-shadow: 0 3px 2px #dee2e6;
        color: #495057;
        font-size: 18px;
        .completed{
            position: relative;
            overflow: hidden;
            opacity: .4;
            text-decoration: line-through;
            transition: opacity .2s ease-in-out;
        }
    }
</style>