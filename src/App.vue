<template>
  <div class="container">
    <header>
      <h1>Todo List</h1>
      <form class="newTodo">
        <input type="text" v-model="newTodo" />
        <Button @click="addTodo" label="Add Todo" type="submit" />
      </form>
      <br />
      <Button v-if="showCompleted" @click="toggleShowCompleted" label="Hide Completed" />
      <Button v-else @click="toggleShowCompleted" label="Show Completed" />
    </header>
    <TodoList :todos="todos" :toggleCompleted="toggleCompleted" :showCompleted="showCompleted" />
  </div>
</template>

<script>
import axios from 'axios'
import TodoList from './components/TodoList'

export default {
  name: 'App',
  components: { TodoList },
  data() {
    return {
      todos: [],
      showCompleted: false,
      newTodo: ''
    }
  },
  created() {
    console.log('created')
    axios
      .get(`${process.env.VUE_APP_SERVER_URL}/todos/`)
      .then(res => {
        console.log(res)
        this.todos = res.data
      })
      .catch(err => console.log(err))
  },
  methods: {
    toggleCompleted(todo) {
      todo.isCompleted = !todo.isCompleted
      axios
        .put(`${process.env.VUE_APP_SERVER_URL}/todos/${todo.id}`, {
          isCompleted: todo.isCompleted
        })
        .then(res => console.log(res))
        .catch(err => console.log(err))
    },
    toggleShowCompleted() {
      this.showCompleted = !this.showCompleted
    },
    addTodo(e) {
      e.preventDefault()
      if (this.newTodo !== '') {
        const id = this.todos.length ? this.todos[this.todos.length - 1].id + 1 : 1
        this.todos.push({
          id,
          task: this.newTodo,
          isCompleted: false
        })
        axios
          .post(`${process.env.VUE_APP_SERVER_URL}/todos/`, { task: this.newTodo })
          .then(res => console.log(res))
          .catch(err => console.log(err))
        this.newTodo = ''
      }
    }
  }
}
</script>

<style>
#app {
  text-align: center;
}
body {
  margin: 0;
}
.container {
  background: #eee;
  margin: 0 auto;
  padding: 2rem 0;
  width: 70%;
  height: 100vh;
  overflow-y: 'scroll';
}
header {
  height: 150px;
}
.container h1 {
  margin-top: 0;
}
.newTodo {
  display: flex;
  justify-content: space-between;
  margin: 0 auto;
  width: 80%;
  max-width: 600px;
}
.newTodo input {
  flex-grow: 1;
  margin-right: 2rem;
}
</style>
