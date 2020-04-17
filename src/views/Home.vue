<template>
  <div id="app">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <p id="authorText"> - By {{author}} </p>

    <AddTodo v-on:add-todo="addTodo" />

    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import HelloWorld from '../components/HelloWorld.vue';
import Todos from '../components/Todos.vue';
import AddTodo from '../components/AddTodo.vue';
import axios from 'axios';

export default {
  name: 'Home',

  components: {
    HelloWorld,
    Todos,
    AddTodo
  },

  data() {
    return {
      author: 'Ashwin Dinesh',
      todos: [
        /*{
          id: 1,
          title: 'Learn exoplayer audio',
          completed: false
        },
        {
          id: 2,
          title: 'Learn exoplayer video',
          completed: false
        },
        {
          id: 3,
          title: 'Learn vuex',
          completed: false
        },
        {
          id: 4,
          title: 'Learn vue js',
          completed: true
        }*/
      ]
    }
  },

  methods: {
    deleteTodo(id) {
      //this.todos = this.todos.filter((todo) => todo.id !== id);

      // Delete at JSON placeholder
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => {
          console.log(res.data);
          this.todos = this.todos.filter((todo) => todo.id !== id);
        })
        .catch(err => console.log(err));
    },

    addTodo(newTodo) {
      //this.todos = [... this.todos, newTodo];

      // Post to JSON placeholder
      const {title, completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then((res) => {
          this.todos = [... this.todos, res.data];
        })
        .catch(err => console.log(err));
    }
  },

  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then((res) => {
        this.todos = res.data;
      })
      .catch((err) => {
        console.log(err);
      });
  }
}
</script>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
}

#authorText {
    text-align: right;
    margin: 12px;
}

img {
    display: block;
    margin-left: auto;
    margin-right: auto;
    margin-top: 12px;
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
