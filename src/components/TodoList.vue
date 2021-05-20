<template>
  <div>
    <ul>
      <li v-for="todo in todos" :key="todo.id" class="todo">
        <h3>{{ todo.task }}</h3>
        <Button
          icon="pi pi-check"
          class="p-button-rounded"
          :class="{ 'p-button-outlined': todo.isCompleted }"
          @click="toggleCompleted(todo)"
        />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['todos', 'toggleCompleted'],
};
</script>

<style>
.todo {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 300px;
  margin: 0 auto;
}
</style>
