<template>
  <div class="flex flex-col space-y-2 md:space-y-4">
    <add-todo @todo-added="todoAdd" />
    <todo-filter
      :todos="todos"
      :active-tab="activeTab"
      @filtered="filterTodos"
    />
    <div
      v-if="todos.length && activeTab === 'all'"
      class="flex flex-col space-y-2 sm:space-y-4 md:space-y-6 lg:space-y-8"
    >
      <todo-single
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @todo-toggled="toggleTodo"
      />
    </div>
    <div
      v-else-if="completedTodos.length && activeTab === 'completed'"
      class="flex flex-col space-y-2 sm:space-y-4 md:space-y-6 lg:space-y-8"
    >
      <todo-single
        v-for="todo in completedTodos"
        :key="todo.id"
        :todo="todo"
        @todo-toggled="toggleTodo"
      />
    </div>
    <div
      v-else-if="pendingTodos.length && activeTab === 'pending'"
      class="flex flex-col space-y-2 sm:space-y-4 md:space-y-6 lg:space-y-8"
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
<script setup lang="ts">
import type { Ref } from 'vue'
import { computed, ref } from 'vue'
import TodoSingle from './TodoSingle.vue'
import AddTodo from './AddTodo.vue'
import TodoFilter from './TodoFilter.vue'
import type { Todo } from '@/types/todo'

const todos: Ref<Todo[]> = ref([])
const activeTab: Ref<string> = ref('all')

const completedTodos = computed(() => {
  return todos.value.filter((todo: Todo) => todo.completed)
})
const pendingTodos = computed(() => {
  return todos.value.filter((todo: Todo) => !todo.completed)
})

function todoAdd(todo: Todo) {
  todos.value.push(todo)
}

function filterTodos(tab: string) {
  activeTab.value = tab
}

function toggleTodo(todo: Todo) {
  const todoIndex = todos.value.findIndex(t => t.id === todo.id)
  if (todoIndex >= 0) todos.value.splice(todoIndex, 1, todo)
}
</script>
