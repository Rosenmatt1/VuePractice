<template>
  <div id="app">
    <AddToDo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from '../components/Todos'
import AddToDo from '../components/AddToDo'
import axios from "axios"

export default {
  name: 'Home',
  components: {
    Todos,
    AddToDo
  },
  mounted() {
    console.log("Mounted Method")
  },
   created() {
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(res => this.todos = res.data)
        .catch(err => console.log(err))
      // fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      //   .then(response => response.json())
      //   .then(json => this.todos = json.data)
      //   console.log(this.todos)
    },
  data() {
    return {
      todos: [],
      attribute: "tester"
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`http://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err =>console.log(err))
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err =>console.log(err))
    }
  },
 
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: 'Avenir', Helvetica, sans-serif;
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
