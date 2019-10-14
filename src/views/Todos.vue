<template>
  <div>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo @add-todo="addTodo" class="todo-form"/>
    <select class="todo-select" v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <Loader v-if="loading"/>
    <TodoList
      v-else-if="filteredTodos.length"
      :todos="filteredTodos" 
      @remove-todo="removeTodo" 
    />
    <p v-else>No Todos!</p>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddTodo from "@/components/AddTodo";
import Loader from "@/components/Loader";

export default {
  name: "app",
  data: () => ({
    todos: [],
    loading: true,
    filter: 'all'
  }),
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then(response => response.json())
      .then(json => {
        this.todos = json
        this.loading = false
      });
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos
      }

      if (this.filter === 'completed') {
        return this.todos.filter(todo => todo.completed)
      }

      if (this.filter === 'not-completed') {
        return this.todos.filter(todo => !todo.completed)
      }
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  }
};
</script>

<style scoped>
  .todo-form {
    margin-bottom: 1rem;
  }

  .todo-select {
    margin-bottom: 2rem;
  }
</style>