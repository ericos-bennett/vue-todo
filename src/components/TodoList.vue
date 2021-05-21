<template>
  <ul class="todoList">
    <li
      v-for="todo in todos"
      :key="todo.id"
      v-show="showCompleted || !todo.isCompleted"
      class="todo"
    >
      <h3>{{ todo.task }}</h3>
      <Button
        icon="pi pi-check"
        class="p-button-rounded"
        :class="{ 'p-button-outlined': !todo.isCompleted }"
        @click="toggleCompleted(todo)"
      />
    </li>
  </ul>
</template>

<script>
export default {
  props: ['todos', 'toggleCompleted', 'showCompleted']
}
</script>

<style>
.todoList {
  padding: 0;
}
.todo {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 600px;
  margin: 0 auto;
}
</style>
