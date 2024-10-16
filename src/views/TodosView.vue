<script setup>
import { uid } from "uid";
import { ref } from "vue";
import TodoCreator from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";

const todoList = ref([]);

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(), // Buat id unik untuk setiap todo
    todo,
    isCompleted: false,
    isEditing: null,
  });
};
</script>

<template>
  <main>
    <h1>Buat List</h1>
    <TodoCreator @create-todo="createTodo" />
    <ul class="todo-list">
      <!-- Tambahkan key dan prop todo -->
      <TodoItem v-for="todo in todoList" :key="todo.id" :todo="todo" />
    </ul>
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
  .todo {
    flex: 1;

    input[type="text"] {
      width: 100%;
      padding: 2px 6px;
      border: 2px solid #41b080;
    }
  }

  .todo-actions {
    display: flex;
    gap: 6px;
    opacity: 0;
    transition: 150ms ease-in-out;
    .icon {
      cursor: pointer;
    }
  }
}
</style>
