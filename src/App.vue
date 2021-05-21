<template>
  <h1>Todo List</h1>
  <TodoList :todos="todos" :toggleCompleted="toggleCompleted" :showCompleted="showCompleted" />
  <form>
    <input type="text" v-model="newTodo" />
    <Button @click="addTodo" label="Add Todo" />
  </form>
  <br />
  <Button v-if="showCompleted" @click="toggleShowCompleted" label="Hide Completed" />
  <Button v-else @click="toggleShowCompleted" label="Show Completed" />
</template>

<script>
import TodoList from './components/TodoList'

export default {
  name: 'App',
  components: { TodoList },
  data() {
    return {
      todos: [
        {
          id: 1,
          task: 'Buy shoelaces',
          isCompleted: false
        },
        {
          id: 2,
          task: 'Pack boxes',
          isCompleted: true
        }
      ],
      showCompleted: false,
      newTodo: ''
    }
  },
  methods: {
    toggleCompleted(todo) {
      todo.isCompleted = !todo.isCompleted
    },
    toggleShowCompleted() {
      this.showCompleted = !this.showCompleted
    },
    addTodo() {
      const id = this.todos[this.todos.length - 1].id + 1
      this.todos.push({
        id,
        task: this.newTodo,
        isCompleted: false
      })
      this.newTodo = ''
    }
  }
}
</script>

<style>
#app {
  text-align: center;
}
form {
  display: flex;
  justify-content: space-between;
  width: 600px;
  margin: 0 auto;
}
</style>
