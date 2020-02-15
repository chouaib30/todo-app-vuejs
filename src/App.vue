<template>
  <div id='app'>
    <img alt='Vue logo' class='logo' src='./assets/logo.png'>
    <h1 class='font-weight-bold'>Vuejs Todo App</h1>
    <Todo />
  </div>
</template>

<script>
  import Todo from './components/Todo.vue'
  export default {
    name: 'App',
    components: {
      Todo
    }
  }
</script>

<style lang='scss'>
  @import url('https://fonts.googleapis.com/css?family=Poppins:400,700&display=swap');
  @import url('https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.4.1/css/bootstrap.min.css');
  @import url('https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.2/animate.min.css');

  .logo{
    width: 120px;
  }

  body{
    background: #f1f3f5;
  }
  
  #app {
    font-family: 'Poppins', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
