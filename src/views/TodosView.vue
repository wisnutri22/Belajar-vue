<script setup>
import { uid } from "uid";
import { ref } from "vue";
import { Icon } from "@iconify/vue";
import TodoCreator from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";

const todoList = ref([]);

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(), // Create a unique id for each todo
    todo,
    isCompleted: false,
    isEditing: null,
  });
};

const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
};

const updateTodo = (updatedTodo, index) => {
  todoList.value[index].todo = updatedTodo;
};
</script>

<template>
  <main>
    <h1>Buat List</h1>
    <TodoCreator @create-todo="createTodo" />
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItem 
        v-for="(todo, index) in todoList"
        :key="todo.id" 
        :todo="todo"
        :index="index"
        @toggle-complete="toggleTodoComplete"
        @update-todo="updateTodo" 
      />
    </ul>
    <p class="todos-msg" v-else>
      <Icon icon="cib:happycow" width="50" height="50" style="color: #36bfa8" />
      <span>Engga punya list buat diberesin! Tambahin dong!</span>
    </p>
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

  .todos-msg {
    display: flex; /* Flexbox for centering */
    align-items: center;
    justify-content: center; /* Center the content */
    gap: 8px;
    margin-top: 24px;
    text-align: center; /* Center the text */
  }
}
</style>
