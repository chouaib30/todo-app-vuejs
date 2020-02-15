<template>
    <div class='container'>
        <TodoList :todos='todos' />
        <AddTodo v-on:addTodo='addNewTodo' />
    </div>
</template>

<script>
    import TodoList from './todo-components/TodoList.vue'
    import AddTodo from './todo-components/AddTodo.vue'

    export default {
    name:'Todo',
    components:{
        TodoList,
        AddTodo,
    },
    data() {
            return {
                todos: [
                    {
                        'id':1,
                        'title':'Learn Bootstrap 4 & Reactjs 😉😉😉😉',
                        'completed':false,
                        'edit': false
                    },
                    {
                        'id':2,
                        'title':'Take Nodejs course 😊😊😊',
                        'completed':false,
                        'edit': false
                    },
                    {
                        'id':3,
                        'title':'Learn vuejs today 🥰🥰🥰',
                        'completed':false,
                        'edit': false
                    }
                ]
            }
        },
        methods : {
            addNewTodo(newTodo){
                this.todos.push({
                    id : newTodo.id,
                    title : newTodo.title,
                    completed : false,
                    edit : false
                })
            }
        }
    }
</script>

<style lang='scss' scoped>

</style>