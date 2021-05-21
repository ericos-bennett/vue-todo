<template>
  <h1>Todo List</h1>
  <TodoList
    :todos="todos"
    :toggleCompleted="toggleCompleted"
    :showCompleted="showCompleted"
  />
  <Button
    v-if="showCompleted"
    @click="toggleShowCompleted"
    label="Hide Completed"
  />
  <Button v-else @click="toggleShowCompleted" label="Show Completed" />
</template>

<script>
import TodoList from './components/TodoList';

export default {
  name: 'App',
  components: { TodoList },
  data() {
    return {
      todos: [
        {
          id: 1,
          task: 'Buy shoelaces',
          isCompleted: false,
        },
        {
          id: 2,
          task: 'Pack boxes',
          isCompleted: true,
        },
      ],
      showCompleted: false,
    };
  },
  methods: {
    toggleCompleted(todo) {
      todo.isCompleted = !todo.isCompleted;
    },
    toggleShowCompleted() {
      this.showCompleted = !this.showCompleted;
    },
  },
};
</script>

<style>
#app {
  text-align: center;
}
</style>
