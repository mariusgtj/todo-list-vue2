<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos 
      v-bind:todos="todos"
      v-on:del-todo="deleteTodo"
    />
  </div>
</template>

<script>
import Header from './components/layout/Header.vue';
import Todos from './components/Todos.vue';
import AddTodo from './components/AddTodo.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Header,
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    // ***Delete
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console.log(err))
    },
    // deleteTodo(id) {
    //   this.todos = this.todos.filter(todo => todo.id !== id)
    // },
    // deleteTodo: function(id) {
    //   return this.todos = this.todos.filter(item => item.id !== id)
    // },

    // ***Create
    // addTodo(newTodo) {
    //   this.todos = [...this.todos, newTodo]
    // }
    addTodo(newTodo) {
      // object destructuring
      const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data]) // i=jsonplaceholder will provide also the id of the new todo and so we will be able to add it to the UI.
        .catch(err => console.log(err));
    }
  },
  created() { // this method executes when page loads
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err));
  }
}
</script>

<style>
  *, *::before, *::after {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
</style>
