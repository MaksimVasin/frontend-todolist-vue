<template>
  <div id = "app">
    <h1>TodoList</h1>
    <AddTodo
      @add-todo="addTodo"
    />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <Loader v-if="loading"/>
    <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>No todos D:</p>

    <!-- <router-view /> -->
  </div>
</template>

<script>

import TodoList from '@/components/TodoList.vue'
import AddTodo from '@/components/AddTodo.vue'
import Loader from '@/components/Loader.vue'
export default {
  name: 'App',
  data() {
    return {
      todos: [
        /* {id: 1, title: "Buy apple", completed: false},
        {id: 2, title: "Buy orange", completed: false},
        {id: 3, title: "Buy red", completed: false}, */
      ],
      loading: true,
      filter: "all",
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => response.json())
      .then(json => {
        json.filter(t => t.completed == true).forEach(element => {
          element.completed = false;
        });
        setTimeout(() => {
          this.todos = json;
          this.loading = false;
        }, 1500) // Timeout for loader, delete
        
      })
  },
  /* watch: {
    filter(value) {

    }
  }, */
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos;
      }
      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed);
      }
      if (this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed);
      }
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },

    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  max-width: 1000px;
  margin: 0 auto;
}
</style>
