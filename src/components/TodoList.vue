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
  margin: 0 auto;
  padding: 0;
  width: 80%;
  max-width: 600px;
  height: calc(100vh - 150px - 4rem);
  overflow-y: scroll;
}
.todo {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-right: 1rem;
}
.todo h3 {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: calc(100% - 4rem);
  margin-right: 1rem;
}
</style>
