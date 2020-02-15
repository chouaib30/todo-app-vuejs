<template>
    <form class='form-inline mx-auto'>
        <input type='text' class='form-control mr-2 p-4' v-model='title'  placeholder='What needs to be done ?'>
        <button @click.prevent='addTodo' class='btn btn-success btn-lg'>Add New Task</button>
    </form>
</template>

<script>
export default {
    name:'AddTodo',
    data(){
        return{
            title: '',
            id: 4
        }
    },
    methods:{
        addTodo(){
            if( this.title.trim().length == 0 ){
                return
            }
            let newTodo = {
                id : this.id,
                title : this.title
            }
            this.$emit('addTodo',newTodo)
            this.id++
            this.title = ''
        }
    }
}
</script>

<style lang='scss' scoped>
    .form-inline{
        display: flex;
        justify-content: space-between;
        width: 70%;
        .form-control{
            width: 70%;
            color: #495057;
        }
        .btn{
            width: 28%;
        }
    }
</style>