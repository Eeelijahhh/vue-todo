<template>
  <div>
    <ul>
      <TodoItem 
        v-for="(todo, index) of todos"
        :todo="todo"
        :index="index"
        :key="todo.id"
        @remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'

export default {
  props: ['todos'],
  components: {
    TodoItem
  },
  methods: {
    removeTodo(id) {
      this.$emit('remove-todo', id)
    }
  }
}
</script>

<style scoped>
  ul {
    list-style: 0;
    margin: 0;
    padding: 0;
  }
</style>