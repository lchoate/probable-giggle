<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
  import AddTodo from '../components/AddTodo';
  import Todos from '../components/Todos';
  import axios from 'axios';

  export default {
    name: 'app',
    components: {
      Todos,
      AddTodo,
    },
    data() {
      return {
        todos: [

        ],
        msg: 'Hello'
      }
    },
    methods: {
      deleteTodo(id){
        console.log('fired');
        axios.delete(`https://jsonplaceholder.typicode.com/todos/$id`)
                .then(this.todos = this.todos.filter(todo => todo.id !== id))
                .catch(err => console.log(err));
      },
      addTodo(newTodo){
        const { title, completed } = newTodo;
        axios.post('https://jsonplaceholder.typicode.com/todos',
                {
                  title,
                  completed
                })
                .then(res =>this.todos = [...this.todos, res.data])
                .catch(err => console.log(err));
        //this.todos = [...this.todos, newTodo];
      },
    },
    created(){
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
              .then(res => this.todos = res.data)
              .catch(err => console.log(err));
    }
  }
</script>

<style>

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  #App {
    font-family: 'Roboto', sans-serif;
  }
</style>
