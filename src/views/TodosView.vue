<script setup>
import { uid } from "uid";
import { ref, watch, computed } from "vue"; // Pastikan watch diimpor dengan benar
import { Icon } from "@iconify/vue";
import TodoCreator from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";

// Initialize todoList
const todoList = ref([]);

// Watch for changes in todoList and save to localStorage
watch(
  todoList,
  () => {
    setTodoListLocalstorage();
  },
  { deep: true }
);

const todoCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted);
});

// Fetch todo list from local storage when the component loads
const fetchTodoList = () => {
  const savedTodolist = JSON.parse(localStorage.getItem("todoList"));
  if (savedTodolist) {
    todoList.value = savedTodolist;
  }
};

// Call fetchTodoList to load initial todos
fetchTodoList();

// Save the todo list to local storage
const setTodoListLocalstorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

// Create a new todo
const createTodo = (todo) => {
  todoList.value.push({
    id: uid(), // Create a unique id for each todo
    todo,
    isCompleted: false,
    isEditing: null,
  });
};

// Toggle the completion status of a todo
const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
};

// Update an existing todo
const updateTodo = (updatedTodo, index) => {
  todoList.value[index].todo = updatedTodo;
};

// Toggle the edit state of a todo
const toggleEditTodo = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
};

// Delete a todo
const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
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
        @edit-todo="toggleEditTodo"
        @delete-todo="deleteTodo"
      />
    </ul>
    <p class="todos-msg" v-else>
      <Icon icon="cib:happycow" width="50" height="50" style="color: #36bfa8" />
      <span>Engga punya list buat diberesin! Tambahin dong!</span>
    </p>
    <p v--if="todoCompleted && todoList.length > 0" class="todos-msg">
    <Icon icon="noto-v1:party-popper" />
    <span> Mantap Semua Beres!</span>
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
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
    text-align: center;
  }
}
</style>
