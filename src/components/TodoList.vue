<template>
  <div class="flex flex-col space-y-2 md:space-y-4">
    <add-todo @todo-added="todoAdd" />
    <todo-filter
      :todos="todos"
      @filtered="filterTodos"
      :active-tab="activeTab"
    />
    <div
      class="flex flex-col space-y-2 sm:space-y-4 md:space-y-6 lg:space-y-8"
      v-if="todos.length && activeTab === 'all'"
    >
      <todo-single
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @todo-toggled="toggleTodo"
      />
    </div>
    <div
      class="flex flex-col space-y-2 sm:space-y-4 md:space-y-6 lg:space-y-8"
      v-else-if="completedTodos.length && activeTab === 'completed'"
    >
      <todo-single
        v-for="todo in completedTodos"
        :key="todo.id"
        :todo="todo"
        @todo-toggled="toggleTodo"
      />
    </div>
    <div
      class="flex flex-col space-y-2 sm:space-y-4 md:space-y-6 lg:space-y-8"
      v-else-if="pendingTodos.length && activeTab === 'pending'"
    >
      <todo-single
        v-for="todo in pendingTodos"
        :key="todo.id"
        :todo="todo"
        @todo-toggled="toggleTodo"
      />
    </div>
    <div v-else class="border border-primary p-2 md:p-4 text-center">
      No todos to display!
    </div>
  </div>
</template>
<script setup>
import TodoSingle from "./TodoSingle.vue";
import AddTodo from "./AddTodo.vue";
import TodoFilter from "./TodoFilter.vue";
import { ref, computed } from "vue";

const todos = ref([]);
const activeTab = ref("all");

const completedTodos = computed(() => {
  return todos.value.filter((todo) => todo.completed);
});
const pendingTodos = computed(() => {
  return todos.value.filter((todo) => !todo.completed);
});

function todoAdd(todo) {
  todos.value.push(todo);
}

function filterTodos(tab) {
  activeTab.value = tab;
}

function toggleTodo(todo) {
  const todoIndex = todos.value.findIndex((t) => t.id === todo.id);
  if (todoIndex >= 0) {
    todos.value.splice(todoIndex, 1, todo);
  }
}
</script>
