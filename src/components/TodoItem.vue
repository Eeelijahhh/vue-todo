<template>
  <li class="todo-item">
    <span :class="{done: todo.completed}">
      <input 
        class="todo-input" 
        type="checkbox"
        :id="index"
        @change="todo.completed = !todo.completed"
        :checked="todo.completed"
      >
      <strong class="todo-count">{{ index + 1 }}</strong>
      <label :for="index">{{ todo.title | uppercase }}</label>
    </span>
    <button class="todo-btn" @click="$emit('remove-todo', todo.id)">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase()
    }
  }
}
</script>

<style scoped>
  .todo-item {
    display: flex;
    justify-content: space-between;
    border: 1px solid #ccc;
    padding: 0.5rem 2rem;
    margin-bottom: 1rem;
  }

  .done {
    text-decoration: line-through;
  }

  .todo-input {
    margin-right: 1rem;
  }

  .todo-count {
    margin-right: .5rem;
  }

  .todo-btn {
    background-color: red;
    color: #fff;
    font-weight: 700;
    border-radius: 50%;
    border: none;
    cursor: pointer;
    outline: none;
  }
</style>