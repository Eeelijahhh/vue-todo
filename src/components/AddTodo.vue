<template>
  <form @submit.prevent="submitHandler">
    <input type="text" v-model="title">
    <button type="submit">Create</button>
  </form>
</template>

<script>
export default {
  data: () => ({
    title: ''
  }),
  methods: {
    submitHandler() {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false
        }

        this.$emit('add-todo', newTodo)

        this.title = ''
      }
    }
  }
}
</script>