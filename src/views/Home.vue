<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" 
      v-on:del-todo="deleteTodo" 
      v-on:mark-todo="markTodo" />
  </div>
</template>

<script>
import Header from "../components/layout/Header.vue";
import Todos from "../components/Todos.vue";
import AddTodo from '../components/AddTodo.vue';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Header,
    Todos,
    AddTodo,
  },
  data(){
    return {
      todos: [

      ],
    }
  },
  methods: {
    deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(() => this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err));
      // not needed anymore, moved to promise above
      //this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo)
    {
      const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', 
      {
        title: title,
        completed: completed
      })
      .then(res => this.todos = [...this.todos, res.data]) // res.data is newTodo basically
      .catch(err => console.log(err));

      // not needed 
      //this.todos = [...this.todos, newTodo];
    },
    markTodo(tid)
    {
      this.todos.forEach(function(element){
        if(element.id === tid)
        {
          element.completed = !element.completed;
        }
      });
    }
  },
  // on page load, when app has been created
  created () {
    // returns promise with todos data from jsonplaceholder API
    // normally it should be our backend api
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5') 
    .then(res => this.todos = res.data) // fil todos with request
    .catch(err => console.log(err));
  }

}
</script>

<style>
  *{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body{
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }


</style>
